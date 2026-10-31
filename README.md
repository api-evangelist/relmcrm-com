# Relm

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

Relm is an API-first CRM built for LLMs and AI agents, operated by ASP FZE LLC (Sharjah, UAE) with data hosted in Helsinki, Finland. Contacts, companies, deals, activities, pipelines, automations, drip sequences, templates and webhooks are exposed three ways over one workspace key: a 72-operation OpenAPI 3.1 REST API at https://api.relmcrm.com/v1, a hosted Streamable-HTTP MCP server at https://api.relmcrm.com/mcp whose 41 typed tools answer an anonymous tools/list, and an A2A 0.3.0 agent card at https://relmcrm.com/.well-known/agent-card.json backed by a JSON-RPC endpoint at https://api.relmcrm.com/a2a. Auth is a workspace bearer key (relm_live_ / free isolated relm_test_) or OAuth 2.1 with PKCE and RFC 7591 dynamic client registration; errors are RFC 9457 problem+json carrying valid_options and a suggestion so an agent self-corrects; writes carry Idempotency-Key on the core creates and If-Match optimistic concurrency on updates. Priced per API request (Free 1,000/mo, Pro $29 for 100,000, Scale $249 for 2,000,000) rather than per seat. The web dashboard is described by the provider as "the thin part".

**Areas:** CRM · Sales · Contacts · Deals · Sales Pipeline · Automation · Webhook · MCP · A2A · AI Agents · Agent-Native · United Arab Emirates

## Relm on APIs.io

Everything profiled for Relm is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/relmcrm-com/](https://apis.io/providers/relmcrm-com/)** — or go straight to one of the APIs or properties below.

### APIs (16)

- [Relm MCP Server](https://apis.io/apis/relmcrm-com/relm-mcp-server/) — First-party hosted Model Context Protocol server (Streamable HTTP) at https://api.relmcrm.com/mcp. 41 typed tools covering every REST capability — schema…
- [Relm A2A Agent](https://apis.io/apis/relmcrm-com/relm-a2a-agent/) — Agent2Agent (A2A 0.3.0) JSON-RPC endpoint at https://api.relmcrm.com/a2a. A message/send whose data part is {tool, arguments} runs one of the same 41 MCP…
- [Relm Activities API](https://apis.io/apis/relmcrm-com/relmcrm-com-activities-api/) — The Activities API from Relm — 3 operation(s) for activities.
- [Relm Automations API](https://apis.io/apis/relmcrm-com/relmcrm-com-automations-api/) — The Automations API from Relm — 3 operation(s) for automations.
- [Relm Batch API](https://apis.io/apis/relmcrm-com/relmcrm-com-batch-api/) — The Batch API from Relm — 1 operation(s) for batch.
- [Relm Companies API](https://apis.io/apis/relmcrm-com/relmcrm-com-companies-api/) — The Companies API from Relm — 3 operation(s) for companies.
- [Relm Connections API](https://apis.io/apis/relmcrm-com/relmcrm-com-connections-api/) — The Connections API from Relm — 2 operation(s) for connections.
- [Relm Contacts API](https://apis.io/apis/relmcrm-com/relmcrm-com-contacts-api/) — The Contacts API from Relm — 3 operation(s) for contacts.
- [Relm Deals API](https://apis.io/apis/relmcrm-com/relmcrm-com-deals-api/) — The Deals API from Relm — 3 operation(s) for deals.
- [Relm Discovery API](https://apis.io/apis/relmcrm-com/relmcrm-com-discovery-api/) — Self-describing schema, usage, settings.
- [Relm Pipelines API](https://apis.io/apis/relmcrm-com/relmcrm-com-pipelines-api/) — The Pipelines API from Relm — 6 operation(s) for pipelines.
- [Relm Registry API](https://apis.io/apis/relmcrm-com/relmcrm-com-registry-api/) — Custom fields, enums, object types.
- [Relm Search API](https://apis.io/apis/relmcrm-com/relmcrm-com-search-api/) — The Search API from Relm — 1 operation(s) for search.
- [Relm Sequences API](https://apis.io/apis/relmcrm-com/relmcrm-com-sequences-api/) — The Sequences API from Relm — 5 operation(s) for sequences.
- [Relm Templates API](https://apis.io/apis/relmcrm-com/relmcrm-com-templates-api/) — The Templates API from Relm — 2 operation(s) for templates.
- [Relm Webhooks API](https://apis.io/apis/relmcrm-com/relmcrm-com-webhooks-api/) — The Webhooks API from Relm — 3 operation(s) for webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Relmcrm Com Webhooks](https://apis.io/asyncapis/relmcrm-com/relmcrm-com-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Relm CRM](https://apis.io/servers/relmcrm-com/relm/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Relmcrm Com Openapi Overlay](https://apis.io/overlays/relmcrm-com/relmcrm-com-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Relmcrm Com Authentication](https://apis.io/security/relmcrm-com/relmcrm-com-authentication/)
- [Relmcrm Com Domain Security](https://apis.io/security/relmcrm-com/relmcrm-com-domain-security/)
- [Relmcrm Com Vulnerability Disclosure](https://apis.io/security/relmcrm-com/relmcrm-com-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Relmcrm Com Scopes](https://apis.io/scopes/relmcrm-com/relmcrm-com-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Relmcrm Com Plans Pricing](https://apis.io/plans/relmcrm-com/relmcrm-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Relmcrm Com Rate Limits](https://apis.io/rate-limits/relmcrm-com/relmcrm-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://relmcrm.com/)
- [Documentation](https://relmcrm.com/docs)
- [Getting started](https://relmcrm.com/docs)
- [API reference](https://relmcrm.com/docs)
- [Pricing](https://relmcrm.com/#pricing)
- [Sign up](https://app.relmcrm.com/)
- [Support](https://relmcrm.com/support)
- [Changelog](https://relmcrm.com/changelog)
- [Terms of service](https://relmcrm.com/terms)
- [Privacy policy](https://relmcrm.com/privacy)
- [Status](https://relmcrm.com/status)

## API Evangelist rating

**Kin Score 64.6** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 54.3 |
| Contract governance | 18.2 |
| Operational transparency | 50.0 |
| Developer ergonomics | 70.8 |
| Access clarity | 76.3 |

**Agent readiness 62.6** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | verified |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 55.9** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/relmcrm-com/](https://apis.io/providers/relmcrm-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Relm: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/relmcrm-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
