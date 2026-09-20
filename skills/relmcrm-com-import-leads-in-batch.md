---
generated: '2026-09-19'
method: generated
name: Import leads in batch
description: Load up to 100 records per call with POST /batch, after registering the custom fields and enum values the import needs, and dedupe on email.
api: openapi/relmcrm-com-openapi.yml
operations: [getSchema, createField, createEnumValue, batch, listContacts]
mcp_tools: [relm_describe_schema, relm_create_field, relm_create_enum_value, relm_batch, relm_list]
source: >-
  Grounded in openapi/_original/relmcrm-com-openapi.json. batch requestBody (operations[] max 100; object
  contact|company|deal|activity; method create|update|delete; data / patch / id) read from the spec; metering
  and event-silence from https://relmcrm.com/docs and the batch operation summary. Migration guides at
  https://relmcrm.com/learn/migrate-from-hubspot etc. describe the same shape.
---

# Import leads in batch

For migrations (HubSpot, Pipedrive, Salesforce, Attio, Airtable, GoHighLevel) and bulk enrichment drops.

## Auth
- Bearer key as in every skill. Rehearse the whole import with a `relm_test_` key first: test mode is free, unmetered, isolated, and its records auto-delete after 7 days.

## Steps
1. **Read the schema** — `getSchema` (`GET /schema`). Map the source system's properties onto Relm fields; list what is missing.
2. **Register missing fields** — `createField` (`POST /fields`) per custom property: `object`, `key`, `label`, `data_type` (text|number|boolean|date|select|multiselect|currency|reference|email|url), optional `enum_group`. Values are then sent under `custom_fields`.
3. **Register missing enum values** — `createEnumValue` (`POST /enums`) with `group` (e.g. `contact.type`) and `value`. Idempotent — safe to call for every distinct source value.
4. **Write in batches** — `batch` (`POST /batch`) with `operations[]` of up to 100 items: `{ "method": "create", "object": "contact", "data": {...} }`. The response is per-operation with partial success — read every item, not just the HTTP status.
5. **Verify** — `listContacts` (`GET /contacts?limit=100&cursor=...`) with `?q=` or `?email=` spot checks; page with `next_cursor` until `has_more` is false.

## Rules
- `batch` has **no** `Idempotency-Key` parameter. A retried batch after a timeout can double-create up to 100 records. Chunk deterministically, record which chunks succeeded, and rely on email uniqueness (a duplicate contact email returns the existing record) where the object allows.
- Batch is metered **per operation** (100 operations = 100 requests of quota) and is **event-silent**: no webhooks or automations fire for batch writes. If downstream automations must run, use the single creates instead.
- Free plan: 1,000 requests/month, hard stop at 429 `quota_exceeded`; check `getUsage` (`GET /usage`) before a large import.
- 422 `unknown_value` / `unknown_field` inside a batch item carries `valid_options` and `suggestion` like any single write — fix the mapping and resend only the failed items.
- Reversal: soft-delete per record (`method: delete` in a follow-up batch, or the per-object delete operations) and `restore*` to undo; no batch-level rollback exists.
