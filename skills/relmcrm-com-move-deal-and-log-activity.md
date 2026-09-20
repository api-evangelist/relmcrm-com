---
generated: '2026-09-19'
method: generated
name: Move a deal and log the activity
description: Advance a deal to a new stage with optimistic concurrency, then record the call, meeting or note that justified the move — backdated if it already happened.
api: openapi/relmcrm-com-openapi.yml
operations: [getDeal, getPipeline, updateDeal, createActivity, listActivities]
mcp_tools: [relm_get, relm_get_pipeline, relm_update, relm_log_activity, relm_list]
source: >-
  Grounded in openapi/_original/relmcrm-com-openapi.json (IfMatch parameter on updateDeal; ActivityInput
  occurred_at; Pipeline.stages[].type) and the Conventions section of https://relmcrm.com/docs (optimistic
  concurrency, 412 version_conflict). Agent playbooks at https://relmcrm.com/resources use this exact loop.
---

# Move a deal and log the activity

## Auth
- Bearer key or OAuth 2.1 token (scope `crm`). Base `https://api.relmcrm.com/v1`.

## Steps
1. **Read the deal** — `getDeal` (`GET /deals/{id}`). Capture `version`, `pipeline`, `stage`.
2. **Read the pipeline** — `getPipeline` (`GET /pipelines/{key}`) for the ordered `stages[]` with `key`, `label`, `type` (open|won|lost). Pick the target stage key from this list — never guess a stage name.
3. **Move the deal** — `updateDeal` (`PATCH /deals/{id}`) with `{ "stage": "<key>" }` and header `If-Match: <version from step 1>`. A 412 `version_conflict` means someone else changed the deal: re-read and reapply. Moving to a stage whose `type` is `won` or `lost` closes the deal; that is visible on every deal as `stage_type`.
4. **Log the activity** — `createActivity` (`POST /activities`) with `type` (a registered `activity.type` such as note/call/email/meeting/task), `body`, `deal_id` and/or `contact_id`, and `occurred_at` if it happened earlier. Send an `Idempotency-Key`.
5. **Confirm the timeline** — `listActivities` (`GET /activities?deal_id=...`).

## Rules
- `updateDeal` is one of six operations that honour `If-Match` (`updateContact`, `updateCompany`, `updateDeal`, `updateActivity`, `updateTemplate`, `updateWebhook`). Always send it from an agent loop.
- An unknown stage key → 422 `unknown_value` with `valid_options` (the pipeline's stage keys) and a `suggestion`.
- A stage change fires `deal.stage_changed` for webhooks and automations (unless the write came through `batch`).
- Reversal: PATCH the deal back to the previous stage with the new `version`; an activity can be soft-deleted (`deleteActivity`) and restored (`restoreActivity`).
