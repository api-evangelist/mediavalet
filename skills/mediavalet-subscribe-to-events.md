---
name: mediavalet-subscribe-to-events
description: Subscribe to MediaValet SkyHOOK events so an agent is notified when assets, categories, keywords or attributes change, instead of polling the API. Use when building a change-driven integration or keeping an external index in sync with a MediaValet library.
generated: '2026-08-13'
method: generated
source: openapi/mediavalet-webhooks-api-openapi.yml + asyncapi/mediavalet-skyhook-asyncapi.yml + https://docs.mediavalet.com/ (How To Guides > How to Create a webhook for an Event; General Information > SkyHOOK)
api: MediaValet Webhooks API (SkyHOOK)
base_url: https://api.mediavalet.com
operations:
  - getEventsTypes
  - createWebhookSubscription
  - getSubscription
  - updateWebhookSubscription
---

# Subscribe to MediaValet SkyHOOK events

SkyHOOK is MediaValet's event service. It delivers changes either to an HTTPS endpoint you own, or
into a private Azure Event Grid instance. Every message is a **CloudEvents 1.0** envelope.

> **Entitlement check first.** SkyHOOK webhooks are an **Enterprise Plan** feature in the MediaValet
> Developer Portal. On the default Developer Plan these operations are unavailable — polling is the
> only option, and it burns the daily request budget.

## Before you start

```
Authorization: bearer <access_token>
Ocp-Apim-Subscription-Key: <subscription_key>
x-mv-api-version: 1.2
```

## Steps

1. **Enumerate the event types** — `GET /skyhook/events` (`getEventsTypes`).
   Do not hard-code the list; read it. As published today it is:

   | Event type | Fires when |
   |---|---|
   | `Asset.StatusUpdated` | Asset status changed (e.g. to Approved) |
   | `Asset.MediaFileAdded` | A media file was added to an asset |
   | `Asset.KeywordsAdded` | Keywords added to an asset |
   | `Asset.KeywordRemoved` | A keyword removed from an asset |
   | `Asset.AttributesAdded` | Custom attributes added to an asset |
   | `Asset.VideoRenditionsAdded` | Video renditions finished processing |
   | `Category.AssetsAssigned` | Assets assigned to a category |
   | `Category.AssetUnassigned` | An asset unassigned from a category |

2. **Create the subscription** — `POST /skyhook/subscriptions` (`createWebhookSubscription`)
   for an HTTPS webhook, or the Event Grid variant if you are delivering into Azure.

3. **Verify it registered** — `GET /skyhook/subscriptions/list` (`getSubscription`).

4. **Update it** — `PUT /skyhook/subscriptions/{subscriptionID}` (`updateWebhookSubscription`)
   when the endpoint URL or the event selection changes.

## Handling a delivery

Every message has the same envelope; discriminate on `type`:

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "source": "00000000-0000-0000-0000-000000000000",
  "type": "Asset.StatusUpdated",
  "data": {
    "LibraryId": "00000000-0000-0000-0000-000000000000",
    "AssetId": "00000000-0000-0000-0000-000000000000",
    "CurrentVersion": "00000000-0000-0000-0000-000000000000",
    "FileName": "file-name.png",
    "Status": "Approved"
  },
  "time": "2022-05-04T20:49:57.8570052+00:00",
  "specversion": "1.0",
  "dataschema": "#",
  "subject": "/library/.../assets/.../Asset.StatusUpdated",
  "contenttype": "application/json"
}
```

- `source` is the **library id** — use it to route multi-tenant deliveries.
- `subject` is a resource path you can parse for ids without touching `data`.
- `data` is thin by design. It tells you *what changed*, not the new state of the asset. Follow up
  with `GET /assets/{assetId}` when you need the full record.
- **Deduplicate on `id`.** MediaValet publishes no delivery-guarantee statement, so assume
  at-least-once and make your handler idempotent — the API itself has no idempotency mechanism to
  lean on.
- `dataschema` is currently the literal `"#"`, so there is no per-event schema to fetch. Validate
  against `asyncapi/mediavalet-skyhook-asyncapi.yml` in this repo.

## Why events beat polling here

Video rendition and upload processing are asynchronous — a `202 Accepted` from the upload flow tells
you MediaValet accepted the request, not that the asset is ready. `Asset.MediaFileAdded` and
`Asset.VideoRenditionsAdded` are the correct completion signals.
