---
name: mediavalet-search-assets
description: Find assets in a MediaValet library by keyword, filename, custom attribute, file type or AI-generated cognitive metadata, and page through the results correctly. Use when an agent needs to locate brand, product or campaign assets before acting on them.
generated: '2026-08-13'
method: generated
source: openapi/mediavalet-assets-api-openapi.yml + https://docs.mediavalet.com/ (How To Guides > How to Search for Assets; General Information > Querystring Parameters, Search and Filters)
api: MediaValet Assets API
base_url: https://api.mediavalet.com
operations:
  - retrieveAssetsWithSearchCriteria2
  - retrieveAssetsWithSearchCriteria
  - retrieveAsset
  - retrieveAttributes
  - retrieveKeywords
  - retrieveCategories
---

# Search for assets in MediaValet

## Before you start

```
Authorization: bearer <access_token>
Ocp-Apim-Subscription-Key: <subscription_key>
x-mv-api-version: 1.2
```

Search is a **read** operation — safe to retry.

## Which operation

- `POST /assets/search` (`retrieveAssetsWithSearchCriteria2`) — the real search surface. Use this
  for search by custom attributes, by filename, filtered by file type, or filtered by cognitive
  (AI-generated) metadata. MediaValet's own four search how-to samples all use this one operation
  with different bodies.
- `GET /assets` (`retrieveAssetsWithSearchCriteria`) — collection listing with querystring criteria.
- `GET /assets/{assetId}` (`retrieveAsset`) — once you have an id, fetch the full asset.

## Resolving vocabulary first

Attribute and keyword searches are keyed by **id**, not by display name. Resolve them once and
cache:

- `GET /attributes` (`retrieveAttributes`) — custom metadata field definitions and their data types.
- `GET /keywords` (`retrieveKeywords`) — the controlled keyword vocabulary.
- `GET /categories` (`retrieveCategories`) — the category tree.

## Paging

Universal on every endpoint, case-insensitive:

```
?count=50&offset=0
```

`count` defaults to **50**, `offset` to **0**. Read the loop bound off the response rather than
probing for the end:

```json
"RecordCount": { "TotalRecordsFound": 812, "StartingRecord": 1, "RecordsReturned": 50 }
```

Keep requesting until `StartingRecord + RecordsReturned > TotalRecordsFound`. There are no cursors.

## Do NOT use include / exclude / max-length

MediaValet documents `include=`, `exclude=` and `max-length=` for sparse fields and truncation, and
states for each: *"This feature has not been implemented yet."* They will be **silently ignored**
(with a note in `Meta.Warnings`), not rejected. Filter client-side instead.

## Reading the result

Results are in `Payload`. Each asset carries:

- `media` — `thumb`, `small`, `medium`, `large`, `original`, `download`, `streamingManifest`, plus
  `sasExpiry` / `sasRenewal`. **Those media URLs are SAS-signed and expire** — treat them as
  short-lived, never persist them. For a durable public URL use the Direct Links skill.
- `file` — filename, md5, mime type, size, dimensions, frame rate, colour mode.
- `attributes`, `keywords`, `categories`, `relatedassets`.
- `permissions[]` and `_links.functions[]` — what the calling user may actually do with this asset.
  Read these *before* attempting a write so a 403 is predictable rather than discovered.
- `record.version` — versioning state (`islatestversion`, `parentid`, `head`).

## Cost control

Search is the cheapest way to burn a Developer Plan's undocumented daily request budget. Page with
a large `count` rather than many small requests, cache the vocabulary lookups, and prefer SkyHOOK
event subscriptions over polling for change detection.
