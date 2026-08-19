---
name: mediavalet-distribute-with-direct-links
description: Create durable CDN direct links for MediaValet assets so images, video, audio and documents can be embedded outside the DAM without expiring SAS URLs. Use when publishing assets to a website, CMS or campaign.
generated: '2026-08-13'
method: generated
source: openapi/mediavalet-direct-links-api-openapi.yml + https://docs.mediavalet.com/ (How To Guides > How to Generate CDN Links)
api: MediaValet Direct Links API
base_url: https://api.mediavalet.com
operations:
  - createADirectLink
  - retrieveDirectLinks2
  - retrieveAsset
---

# Distribute MediaValet assets with CDN direct links

## The problem this solves

The `media` URLs on an asset (`thumb`, `small`, `large`, `original`, `download`) are **SAS-signed
and expire** — the asset payload even carries `sasExpiry` and `sasRenewal`. Embedding one of those
in a web page or an email produces a link that dies. Direct Links are the durable CDN URLs meant
for distribution outside the DAM.

## Before you start

```
Authorization: bearer <access_token>
Ocp-Apim-Subscription-Key: <subscription_key>
x-mv-api-version: 1.2
```

## Steps

1. **Resolve the asset** — `GET /assets/{assetId}` (`retrieveAsset`).
   Check `permissions[]` for the distribution affordance before you attempt the write; a permission
   failure returns **403** on API version 1.2.

2. **Create the direct link** — `POST /directlinks/{assetId}` (`createADirectLink`).
   The same operation serves image, video, audio and document assets — MediaValet's how-to guide
   presents four variants of the same call, differing only in the body. A `201` carries the created
   link.

   A `400` here can be specifically *"Link name is invalid"* — read `Meta.Errors` rather than
   assuming the whole body was rejected.

3. **List existing links** — `GET /directlinks/{assetId}` (`retrieveDirectLinks2`).
   **Do this before creating.** There is no idempotency key on this API, so calling
   `POST /directlinks/{assetId}` twice can produce two links for the same asset. Read first, create
   only if absent.

## Operational notes

- A direct link is a **distribution decision**, not a metadata edit. Once the URL is public it is
  outside MediaValet's permission model — an agent should treat link creation as an escalation-worthy
  action and record it.
- For a whole curated set rather than a single file, consider a **Branded Portal**
  (`openapi/mediavalet-branded-portals-api-openapi.yml`) — a hosted, branded, permissioned view onto
  a subset of the library, and the largest resource in the API after Assets.
- To embed a *picker* rather than a fixed link, MediaValet ships the Asset Picker iframe component —
  see `components/mediavalet-components.yml`.

## Failure modes

| Status | Meaning | What to do |
|---|---|---|
| 400 | Invalid body, or invalid link name | Read `Meta.Errors`; fix the named field |
| 403 | Not permitted to create links for this asset | Check `permissions[]`; escalate to a library admin |
| 404 | Asset not found, or outside your library | Re-resolve the id via search |
| 204 | *"Library does not contain direct link"* | Not an error — MediaValet uses 204 for absence here, so do not read it as success |
