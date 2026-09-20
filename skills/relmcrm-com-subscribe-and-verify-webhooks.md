---
generated: '2026-09-19'
method: generated
name: Subscribe to and verify webhooks
description: Register an https endpoint for CRM events, store the one-time signing secret, verify Relm-Signature on each delivery, and inspect or pause deliveries.
api: openapi/relmcrm-com-openapi.yml
operations: [createWebhook, getWebhook, listDeliveries, updateWebhook, deleteWebhook]
mcp_tools: [relm_create_webhook, relm_get_webhook, relm_manage_webhook, relm_delete_webhook]
source: >-
  Grounded in openapi/_original/relmcrm-com-openapi.json (Webhooks tag; WebhookInput / Webhook schemas) and the
  Webhooks section of https://relmcrm.com/docs (headers, signature scheme, retry schedule). Catalog in
  asyncapi/relmcrm-com-webhooks.yml.
---

# Subscribe to and verify webhooks

## Auth
- Bearer key. Live-mode webhook URLs must be public https (private, loopback and link-local hosts are rejected); a `relm_test_` key may point at `localhost` for development.

## Steps
1. **Register** — `createWebhook` (`POST /webhooks`) with `url` and `events` — a subset of `contact.created`, `contact.updated`, `deal.created`, `deal.updated`, `deal.stage_changed`, or `["*"]`. The response includes `secret` (`whsec_...`) **once**. Store it now; it is never returned again.
2. **Receive** — each delivery is a JSON POST with headers `Relm-Event`, `Relm-Delivery` and `Relm-Signature: t=<unix>,v1=<hmac>`.
3. **Verify** — compute HMAC-SHA256 over `"<t>.<raw body>"` with the secret and compare to `v1` in constant time. Reject on mismatch. Return 2xx quickly; anything else (or a timeout) is retried.
4. **Inspect** — `listDeliveries` (`GET /webhooks/{id}/deliveries`) shows recent attempts; `getWebhook` (`GET /webhooks/{id}`) the subscription.
5. **Pause or change** — `updateWebhook` (`PATCH /webhooks/{id}`) with `enabled: false` pauses delivery without losing the subscription; send `If-Match` with the webhook's `version` (412 `version_conflict` if stale). `deleteWebhook` removes it — there is no restore for webhooks.

## Rules
- Retries: 1m, 5m, 30m, 2h, 6h — dead-lettered after 6 attempts. Design the receiver to be idempotent on `Relm-Delivery`.
- Bulk writes via `batch` are event-silent: an import will not produce deliveries.
- Subscriptions are per workspace **and mode**; a test-mode webhook never sees live events.
- Lost the secret? Delete and re-create the subscription — rotation is not a separate operation.
