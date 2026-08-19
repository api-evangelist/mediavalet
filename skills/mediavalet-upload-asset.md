---
name: mediavalet-upload-asset
description: Upload a new file into a MediaValet library as an asset, assign it to a category, and finalize it with title, description and metadata. Use when adding new creative, product or brand assets to MediaValet.
generated: '2026-08-13'
method: generated
source: openapi/mediavalet-uploads-api-openapi.yml + https://docs.mediavalet.com/ (How To Guides > How to Upload an Asset)
api: MediaValet Uploads API
base_url: https://api.mediavalet.com
operations:
  - createAsset2
  - completeUpload
  - createAssetAssociationWithCategories
  - updateAsset
---

# Upload an asset to MediaValet

MediaValet ingest is a **three-party** flow: you ask MediaValet for an upload location, you PUT the
bytes directly to Azure Blob Storage (not to `api.mediavalet.com`), then you tell MediaValet the
bytes have landed. Nothing about the asset is durable until the finalize step.

## Before you start

Every request needs **both** credentials:

```
Authorization: bearer <access_token>          # from https://login.mediavalet.com/connect/token
Ocp-Apim-Subscription-Key: <subscription_key> # from your Developer Portal profile
x-mv-api-version: 1.2                         # ALWAYS set this — omitting it pins you to 1.0
```

There is **no idempotency key** on this API. If a step fails ambiguously, `GET /assets/{assetId}`
to check state before retrying — a blind retry of `POST /uploads` creates a second asset.

## Steps

1. **Request an upload URL** — `POST /uploads` (`createAsset2`).
   Send the filename and file size. The response carries the new `assetId` and an `uploadUrl`
   pointing at Azure Blob Storage with a time-limited SAS token.

2. **PUT the bytes to the returned `uploadUrl`.**
   This request goes to Azure, **not** to `api.mediavalet.com`, and it does **not** carry the
   MediaValet credentials — the SAS token in the URL is the authorization. Large files are chunked;
   MediaValet's own "How to upload big files" sample covers the block-upload pattern. The SAS URL
   expires, so do not stage it and upload later.

3. **Complete the upload** — `PUT /uploads/{assetId}` (`completeUpload`).
   Supply the title, description and file size so MediaValet can reconcile what it received against
   what you announced.

4. **Assign the asset to a category** — `POST /uploads/{assetId}/categories`
   (`createAssetAssociationWithCategories`).
   Get valid category ids first from `GET /categories` (`retrieveCategories`). An asset with no
   category is hard for library users to find.

5. **Finalize** — `PATCH /uploads/{assetId}` (`updateAsset`), `Content-Type: application/json-patch+json`.
   Apply the remaining metadata as a JSON Patch document:

   ```json
   [
     { "op": "replace", "path": "/title", "value": "Spring campaign hero" },
     { "op": "replace", "path": "/description", "value": "Hero image, EU launch" }
   ]
   ```

## Checking that it worked

- A `202 Accepted` means MediaValet took the request, **not** that processing finished. Renditions,
  video transcodes and AI metadata are asynchronous.
- **Read `Meta.Errors` and `Meta.Warnings` on every response, including 200s.** A malformed PATCH
  instruction is silently *ignored* and reported there rather than failing the request.
- To know when the asset is really ready, subscribe to the SkyHOOK `Asset.MediaFileAdded` event
  (Enterprise plan) instead of polling — see `asyncapi/mediavalet-skyhook-asyncapi.yml`.

## Failure modes

| Status | Meaning here | What to do |
|---|---|---|
| 400 | Bad payload, or a feature used against the wrong API version | Set `x-mv-api-version: 1.2` explicitly and re-check the body |
| 401 | Token expired, or subscription key missing | Refresh the token; confirm both headers are present |
| 403 | Authenticated but not permitted (1.2 semantics) | Check the `permissions` array on the parent resource; escalate to a library admin |
| 409 | Conflict — the original request may have succeeded | `GET` before retrying |
| 500 | Server-side failure | Backoff, then verify with a `GET` before retrying a write |
