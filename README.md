# MediaValet (mediavalet)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
