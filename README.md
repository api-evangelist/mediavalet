# MediaValet (mediavalet)

MediaValet is a cloud-native digital asset management (DAM) platform, built on Microsoft Azure, for storing, organizing, sharing, and distributing an organization's images, videos, documents, and other brand and marketing assets. Its Open API is a RESTful, JSON, hypermedia-driven service (base `https://api.mediavalet.com`) that lets developers and partners automate uploading, cataloging, searching, and governing assets, categories, attributes, keywords, and users.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/mediavalet/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/mediavalet/refs/heads/main/apis.yml)

## Access Model

The MediaValet Open API is available to MediaValet customers and requires two credentials on every request:

- **OAuth 2.0 (OIDC):** obtain a Bearer access token from `https://login.mediavalet.com/connect/token` (authorization code flow for interactive apps, with `openid api offline_access` scopes; refresh tokens supported).
- **Subscription key:** a per-account key issued through the [MediaValet Developer Portal](https://developer.mediavalet.com/) and sent in the `Ocp-Apim-Subscription-Key` header.

To get started you create an account in the Developer Portal, subscribe to an API plan, and — once the subscription is approved — receive your subscription key by email. The API is fronted by Azure API Management, which throttles per subscription key (HTTP 429 when exceeded). This is not an open, self-service, unauthenticated public API; it is a documented public API gated by a MediaValet subscription. Pricing is enterprise / contact-sales.

## Tags

- Digital Asset Management
- DAM
- Media
- Assets
- Content
- Marketing
- Cloud Storage

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### MediaValet Assets API

Retrieve, update, search, and inspect digital assets and their derivatives — get an asset and its renditions, list related assets, read comments and history, manage per-asset attributes and keywords, and check video intelligence status.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Assets
- Media
- Search

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MediaValet Categories API

Create, list, and read the hierarchical categories that organize a MediaValet library, retrieve the assets filed under a category, and manage category permission sets that govern which users and groups can see and act on each branch of the tree.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Categories
- Organization
- Taxonomy

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MediaValet Attributes API

Define and read custom metadata fields (attributes) for a library and apply or remove attribute values on individual assets, enabling structured, searchable metadata beyond built-in fields.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Attributes
- Metadata
- Custom Fields

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MediaValet Keywords API

Manage the keyword vocabulary used to tag assets — list and read keywords and keyword groups, and add or remove keywords on assets to power search, filtering, and auto-tagging workflows.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Keywords
- Tagging
- Metadata

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MediaValet Uploads API

Ingest new files into a library through the chunked upload workflow — create an upload session, transfer file chunks to the returned storage location, then commit the upload so MediaValet processes the file into a managed asset with renditions.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Uploads
- Ingest
- Files

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MediaValet Users API

Read users, user groups, the current authenticated user and their permissions, and approvers within an organizational unit — the identity and access context that governs who can view and act on assets across the library.

- **Human URL:** [https://docs.mediavalet.com/](https://docs.mediavalet.com/)
- **Base URL:** `https://api.mediavalet.com`

#### Tags

- Users
- Permissions
- Administration

#### Properties

- [Documentation](https://docs.mediavalet.com/)
- [API Reference](https://developer.mediavalet.com/)
- [OpenAPI](openapi/mediavalet-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/mediavalet.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mediavalet.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/mediavalet)
- [Website](https://www.mediavalet.com)
- [Documentation](https://docs.mediavalet.com/)
- [Developer Portal](https://developer.mediavalet.com/)
- [Plans](plans/mediavalet-plans-pricing.yml)
- [Rate Limits](rate-limits/mediavalet-rate-limits.yml)
- [Fin Ops](finops/mediavalet-finops.yml)
- [Blog](https://www.mediavalet.com/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
