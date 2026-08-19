---
name: mediavalet-tag-and-describe-asset
description: Add or update metadata on a MediaValet asset — description, alt text and custom attributes via JSON Patch, and keywords via the keyword association endpoint. Use when enriching assets for search, accessibility or governance.
generated: '2026-08-13'
method: generated
source: openapi/mediavalet-assets-api-openapi.yml + https://docs.mediavalet.com/ (How To Guides > How to Add Metadata to an Image; General Information > PATCH Requests)
api: MediaValet Assets API
base_url: https://api.mediavalet.com
operations:
  - updateAssetWithPatchOperations
  - createAssociationOfAssetsAndKeywords
  - retrieveAttributes
  - retrieveKeywords
  - retrieveAsset
---

# Tag and describe a MediaValet asset

Metadata enrichment is the single highest-value agent job in a DAM, and MediaValet splits it across
two mechanisms that behave differently. Attributes and text fields go through **JSON Patch**;
keywords go through a **dedicated association endpoint**.

## Before you start

```
Authorization: bearer <access_token>
Ocp-Apim-Subscription-Key: <subscription_key>
x-mv-api-version: 1.2
```

Version matters here more than anywhere else in the API. The `Status` attribute data type was added
in **1.1** — submitting a Status attribute against 1.0 (the default when the header is omitted)
returns **400 Bad Request**.

## 1. Resolve the attribute definitions

`GET /attributes` (`retrieveAttributes`) returns the custom metadata field definitions with their
data types. Patch paths are keyed by attribute id, not by label.

## 2. Apply text and attribute changes with JSON Patch

`PATCH /assets/{assetId}` (`updateAssetWithPatchOperations`)
with `Content-Type: application/json-patch+json`:

```json
[
  { "op": "test",    "path": "/description", "value": "" },
  { "op": "replace", "path": "/description", "value": "Product hero, studio lighting, white seamless" },
  { "op": "replace", "path": "/altText",     "value": "A blue running shoe on a white background" }
]
```

MediaValet accepts the six RFC 6902 instructions: `add`, `remove`, `replace`, `test`, `move`,
`copy`. Its `replace` examples also carry a non-standard `oldValue` alongside `value`.

### The trap that matters

MediaValet does **not** apply a patch atomically:

> "If `op` is entered as any value other than an accepted instruction, or if a required field is
> missing from an instruction the line will be ignored, and an error will be added to the response."

So a bad instruction is **skipped, not rejected** — the request still returns success and the rest
of the document still applies. **You must read `Meta.Errors` and `Meta.Warnings` on the response.**
Treating HTTP 200 as "the patch applied" will silently lose metadata.

Use a leading `test` operation when you need optimistic concurrency; there are no ETags on this API.

## 3. Add keywords

Keywords are not patched onto the asset — they are associated:

`POST /assets/{assetId}/keywords` (`createAssociationOfAssetsAndKeywords`)

Resolve valid terms first with `GET /keywords` (`retrieveKeywords`). Keywords carry an
`ApprovalStatus` and an approval audit trail, and they belong to hierarchical keyword groups, so an
agent proposing new vocabulary should expect a governance step rather than immediate publication.

## 4. Verify

`GET /assets/{assetId}` (`retrieveAsset`) and confirm `attributes`, `keywords` and `description`
are what you intended.

## Permissions

Check the asset's `permissions[]` array and `_links.functions[]` before writing. On API version 1.2
a permission failure is **403**, not 401 — do not treat it as an expired token and retry with a
fresh one. On 1.0 and 1.1 the same condition returns 401, so version-aware error handling is
required.

## Retry safety

There is no idempotency key. A `replace` patch is naturally idempotent and safe to retry; a keyword
association is not necessarily so — `GET` the asset first and re-derive the delta rather than
replaying the request.
