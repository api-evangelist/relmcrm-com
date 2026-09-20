---
generated: '2026-09-19'
method: generated
name: Create a contact and open a deal
description: Read the live schema, create (or dedupe) a contact with an Idempotency-Key, link it to a company, and open a deal in the right pipeline stage — the core Relm write path.
api: openapi/relmcrm-com-openapi.yml
operations: [getSchema, createCompany, createContact, createDeal, listPipelines]
mcp_tools: [relm_describe_schema, relm_create, relm_list_pipelines]
source: >-
  Grounded in openapi/_original/relmcrm-com-openapi.json (OpenAPI 3.1.0, 72 operations). Every operationId
  verified verbatim in the spec; auth per authentication/relmcrm-com-authentication.yml, errors per
  errors/relmcrm-com-problem-types.yml, idempotency + concurrency per conventions/relmcrm-com-conventions.yml,
  entity graph per data-model/relmcrm-com-data-model.yml.
---

# Create a contact and open a deal

The marquee Relm flow: a lead arrives, an agent records the person, their company and an opportunity.

## Auth
- `Authorization: Bearer relm_live_...` (or `relm_test_...` to rehearse against the free, isolated test dataset). Base URL `https://api.relmcrm.com/v1`. See `authentication/relmcrm-com-authentication.yml`.
- Over MCP the same steps are `relm_describe_schema`, `relm_list_pipelines`, `relm_create` at `https://api.relmcrm.com/mcp` (OAuth 2.1 or the same key).

## Steps
1. **Read the schema first** — `getSchema` (`GET /schema`). Learn the `contact.type` enum values, the registered custom fields, and each object's `list_filters`. Relm's own instruction is "call this before guessing a type, field or filter".
2. **Find the pipeline and stage** — `listPipelines` (`GET /pipelines`). Note the pipeline `key` (or `pl_` id) and the stage `key` you want; each stage carries `type` open|won|lost.
3. **Create the company** — `createCompany` (`POST /companies`) with `name` and `domain`. Send an `Idempotency-Key` header so a retried request replays instead of duplicating. Keep the returned `cmp_` id.
4. **Create the contact** — `createContact` (`POST /contacts`) with at least one identifier (`email`, `phone` or `linkedin_url`; a name/company/custom field also satisfies `identifier_required`), plus `company_id` from step 3. Send an `Idempotency-Key`. Email is unique per workspace: a duplicate returns the **existing** record (409 `conflict` semantics) — treat that as success, not failure.
5. **Open the deal** — `createDeal` (`POST /deals`) with `title`, `value_cents`, `currency`, `pipeline` (key from step 2), `stage` (key), `company_id`, `primary_contact_id`. Send an `Idempotency-Key`.

## Rules
- Idempotency-Key covers exactly these four creates (`createContact`, `createCompany`, `createDeal`, `createActivity`); same key + different body returns 409 `idempotency_key_reused`.
- Unknown enum value → 422 `unknown_value` with `valid_options` and a `suggestion`: retry with a listed value, or create it via `createEnumValue` (`POST /enums`, idempotent). Unknown top-level field → 422 `unknown_field`: register it with `createField` (`POST /fields`) and send it under `custom_fields`.
- A `company_id` / `primary_contact_id` that does not exist in this workspace **and mode** → 422 `invalid_reference`. Test and live never mix.
- Reversal: each create can be soft-deleted (`deleteContact` / `deleteCompany` / `deleteDeal`) and restored (`restoreContact` / `restoreCompany` / `restoreDeal`); no restore window is published.
