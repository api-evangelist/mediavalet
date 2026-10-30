# MediaValet

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

MediaValet is a cloud-native, Microsoft Azure-based digital asset management (DAM) platform for storing, organizing, governing, sharing and distributing an organization's images, videos, documents and other brand, campaign and product assets. Its Open API is a RESTful, JSON, hypermedia-driven service at https://api.mediavalet.com, fronted by Azure API Management and secured with BOTH an OAuth 2.0 / OpenID Connect bearer token (issuer https://iam.mediavalet.com) and a per-account Ocp-Apim-Subscription-Key. The published surface runs to 312 operations across 29 resources - assets, categories, attributes, keywords, uploads, users, user groups, branded portals, lightboxes, direct/CDN links, downloads, sharing, crops, persons, saved searches, reports, notifications, organizational units and third-party integrations - plus SkyHOOK, an event service that delivers CloudEvents 1.0 messages to a webhook or a private Azure Event Grid instance. API versions are selected per request with the x-mv-api-version header (1.0 default, 1.1, 1.2). MediaValet publishes no OpenAPI; its machine-readable contract is a Postman Collection v2.1.0 at docs.mediavalet.com, from which the definitions in this repo are derived. Access requires an existing MediaValet subscription and an approved Developer Portal account.

**Areas:** Digital Asset Management · Media · Assets · Content · Marketing · Brand Management · Cloud Storage · Metadata · Video · Image · Webhook · Microsoft Azure

## MediaValet on APIs.io

Everything profiled for MediaValet is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/mediavalet/](https://apis.io/providers/mediavalet/)** — or go straight to one of the APIs or properties below.

### APIs (29)

- [MediaValet Assets API](https://apis.io/apis/mediavalet/mediavalet-assets-api/) — Core digital asset objects, their media files, renditions, versions, comments, history, faces and video clips. The centre of the MediaValet data model. 54…
- [MediaValet Categories API](https://apis.io/apis/mediavalet/mediavalet-categories-api/) — Hierarchical categories (folders) that organize assets and carry the permission sets granted to user groups. 18 operations.
- [MediaValet Users API](https://apis.io/apis/mediavalet/mediavalet-users-api/) — Users, their profiles, permissions, entitlements and public self-registration. 18 operations.
- [MediaValet Lightbox API](https://apis.io/apis/mediavalet/mediavalet-lightbox-api/) — Lightboxes — user-curated collections of assets that can be shared by share code. 15 operations.
- [MediaValet Integrations API](https://apis.io/apis/mediavalet/mediavalet-integrations-api/) — Third-party integration registration — apps, allowed origins for iframe embedding, subscriptions, users and entitlements. 12 operations.
- [MediaValet Uploads API](https://apis.io/apis/mediavalet/mediavalet-uploads-api/) — Chunked ingest of new files and new asset versions into a library, via MediaValet-issued Azure blob upload URLs. 11 operations.
- [MediaValet Attributes API](https://apis.io/apis/mediavalet/mediavalet-attributes-api/) — Custom metadata attribute definitions, their data types (including the Status type added in API version 1.1) and embedded-data mappings. 10 operations.
- [MediaValet Reports API](https://apis.io/apis/mediavalet/mediavalet-reports-api/) — Usage and activity reporting across the library. 10 operations.
- [MediaValet Downloads API](https://apis.io/apis/mediavalet/mediavalet-downloads-api/) — Asset download requests, packaged downloads and download presets. 9 operations.
- [MediaValet Notification API](https://apis.io/apis/mediavalet/mediavalet-notification-api/) — In-product notifications and notification preferences. 9 operations.
- [MediaValet Sharing API](https://apis.io/apis/mediavalet/mediavalet-sharing-api/) — Sharing of assets and lightboxes with external recipients by share code. 9 operations.
- [MediaValet Crop API](https://apis.io/apis/mediavalet/mediavalet-crop-api/) — Server-side cropping of image assets, including reusable crop templates. 8 operations.
- [MediaValet Persons API](https://apis.io/apis/mediavalet/mediavalet-persons-api/) — Person and face recognition records used to tag the people appearing in assets. 8 operations.
- [MediaValet Webhooks API](https://apis.io/apis/mediavalet/mediavalet-webhooks-api/) — SkyHOOK webhook and Azure Event Grid subscription management for MediaValet events. 5 operations.
- [MediaValet Authorization API](https://apis.io/apis/mediavalet/mediavalet-authorization-api/) — Authorization and permission checks for the calling user. 3 operations.
- [MediaValet Keywords API](https://apis.io/apis/mediavalet/mediavalet-keywords-api/) — The controlled keyword vocabulary and per-asset tagging, with keyword approval workflow. 3 operations.
- [MediaValet Searches API](https://apis.io/apis/mediavalet/mediavalet-searches-api/) — Search across the library, including the filter and facet grammar. 3 operations.
- [MediaValet Config API](https://apis.io/apis/mediavalet/mediavalet-config-api/) — Library and account configuration. 2 operations.
- [MediaValet Home API](https://apis.io/apis/mediavalet/mediavalet-home-api/) — The hypermedia entry point and the bulk batching endpoint. 2 operations.
- [MediaValet Branded Portals API](https://apis.io/apis/mediavalet/mediavalet-brandedportals-api/) — Branded Portals — externally shareable, branded views onto a subset of the library.
- [MediaValet Introduction And Help API](https://apis.io/apis/mediavalet/mediavalet-introductionandhelp-api/) — Introductory and help resources served by the API.
- [MediaValet Keyword Groups API](https://apis.io/apis/mediavalet/mediavalet-keywordgroups-api/) — Groupings of controlled-vocabulary keywords.
- [MediaValet Reports V2 API](https://apis.io/apis/mediavalet/mediavalet-reportsv2-api/) — Version 2 of the usage and activity reporting surface.
- [MediaValet Attribute Groups API](https://apis.io/apis/mediavalet/mediavalet-attribute-groups-api/) — Groupings of custom metadata attributes.
- [MediaValet Direct Links API](https://apis.io/apis/mediavalet/mediavalet-direct-links-api/) — Direct/CDN links to assets and renditions for external distribution.
- [MediaValet Org unit API](https://apis.io/apis/mediavalet/mediavalet-org-unit-api/) — Organizational units (libraries) and their configuration.
- [MediaValet Saved Searches API](https://apis.io/apis/mediavalet/mediavalet-saved-searches-api/) — Saved searches and their execution.
- [MediaValet Terms And Conditions API](https://apis.io/apis/mediavalet/mediavalet-terms-and-conditions-api/) — Terms and conditions acceptance.
- [MediaValet User Groups API](https://apis.io/apis/mediavalet/mediavalet-user-groups-api/) — User groups and group membership.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [MediaValet SkyHOOK Events](https://apis.io/asyncapis/mediavalet/mediavalet-skyhook-asyncapi/)

#### Event channels (1)

Individual events and webhooks the provider emits.

- [/](https://apis.io/channels/mediavalet/skyhookevents/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [MediaValet DAM (candidate MCP server)](https://apis.io/servers/mediavalet/mediavalet-dam-candidate-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Mediavalet Agentic Access](https://apis.io/agentic-access/mediavalet/mediavalet-agentic-access/)

#### Collections (29)

Postman and Open Collection request collections.

- [MediaValet Assets API](https://apis.io/collections/mediavalet/open-mediavalet-assets-api/)
- [MediaValet AttributeGroups API](https://apis.io/collections/mediavalet/open-mediavalet-attribute-groups-api/)
- [MediaValet Attributes API](https://apis.io/collections/mediavalet/open-mediavalet-attributes-api/)
- [MediaValet Authorization API](https://apis.io/collections/mediavalet/open-mediavalet-authorization-api/)
- [MediaValet BrandedPortals API](https://apis.io/collections/mediavalet/open-mediavalet-branded-portals-api/)
- [MediaValet Categories API](https://apis.io/collections/mediavalet/open-mediavalet-categories-api/)
- [MediaValet Config API](https://apis.io/collections/mediavalet/open-mediavalet-config-api/)
- [MediaValet Crop API](https://apis.io/collections/mediavalet/open-mediavalet-crop-api/)
- [MediaValet DirectLinks API](https://apis.io/collections/mediavalet/open-mediavalet-direct-links-api/)
- [MediaValet Downloads API](https://apis.io/collections/mediavalet/open-mediavalet-downloads-api/)
- [MediaValet Home API](https://apis.io/collections/mediavalet/open-mediavalet-home-api/)
- [MediaValet Integrations API](https://apis.io/collections/mediavalet/open-mediavalet-integrations-api/)
- [MediaValet IntroductionAndHelp API](https://apis.io/collections/mediavalet/open-mediavalet-introduction-and-help-api/)
- [MediaValet KeywordGroups API](https://apis.io/collections/mediavalet/open-mediavalet-keyword-groups-api/)
- [MediaValet Keywords API](https://apis.io/collections/mediavalet/open-mediavalet-keywords-api/)
- [MediaValet Lightbox API](https://apis.io/collections/mediavalet/open-mediavalet-lightbox-api/)
- [MediaValet Notification API](https://apis.io/collections/mediavalet/open-mediavalet-notification-api/)
- [MediaValet OrgUnit API](https://apis.io/collections/mediavalet/open-mediavalet-org-unit-api/)
- [MediaValet Persons API](https://apis.io/collections/mediavalet/open-mediavalet-persons-api/)
- [MediaValet Reports API](https://apis.io/collections/mediavalet/open-mediavalet-reports-api/)
- [MediaValet ReportsV2 API](https://apis.io/collections/mediavalet/open-mediavalet-reports-v2-api/)
- [MediaValet SavedSearches API](https://apis.io/collections/mediavalet/open-mediavalet-saved-searches-api/)
- [MediaValet Searches API](https://apis.io/collections/mediavalet/open-mediavalet-searches-api/)
- [MediaValet Sharing API](https://apis.io/collections/mediavalet/open-mediavalet-sharing-api/)
- [MediaValet TermsAndConditions API](https://apis.io/collections/mediavalet/open-mediavalet-terms-and-conditions-api/)
- …and 4 more published on APIs.io

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Mediavalet Openapi Overlay](https://apis.io/overlays/mediavalet/mediavalet-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Mediavalet Authentication](https://apis.io/security/mediavalet/mediavalet-authentication/)
- [Mediavalet Domain Security](https://apis.io/security/mediavalet/mediavalet-domain-security/)
- [Mediavalet Trust Center](https://apis.io/security/mediavalet/mediavalet-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Mediavalet Scopes](https://apis.io/scopes/mediavalet/mediavalet-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Mediavalet Plans Pricing](https://apis.io/plans/mediavalet/mediavalet-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Mediavalet Rate Limits](https://apis.io/rate-limits/mediavalet/mediavalet-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Mediavalet Finops](https://apis.io/finops/mediavalet/mediavalet-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.mediavalet.com)
- [Documentation](https://docs.mediavalet.com/)
- [Getting started](https://developer.mediavalet.com/getting-started)
- [API reference](https://docs.mediavalet.com/)
- [Pricing](https://www.mediavalet.com/pricing)
- [Sign up](https://developer.mediavalet.com/signup)
- [Support](https://support.mediavalet.com/hc/en-us)
- [Blog](https://www.mediavalet.com/blog)
- [Terms of service](https://www.mediavalet.com/terms-and-condition)
- [Privacy policy](https://www.mediavalet.com/privacy-policy)
- [GitHub](https://github.com/MediaValet)

## API Evangelist rating

**Kin Score 60.2** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 58.9 |
| Contract governance | 18.2 |
| Operational transparency | 34.2 |
| Developer ergonomics | 58.9 |
| Access clarity | 81.6 |

**Agent readiness 33.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | negotiable (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/mediavalet/](https://apis.io/providers/mediavalet/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for MediaValet: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/mediavalet/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
