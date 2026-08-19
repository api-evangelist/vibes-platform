---
name: vibes-platform-send-broadcast
description: >-
  Schedule, inspect, amend or cancel an SMS/MMS/push broadcast to a Vibes subscription list.
  Sending is irreversible once the broadcast leaves the scheduled state.
generated: '2026-08-13'
method: generated
source: openapi/vibes-platform-api-openapi.json, https://developer-platform.vibes.com/reference/broadcast-api-1
api: Vibes Platform API
base_url: https://public-api.vibescm.com
operations:
  - POST /companies/{company_key}/mobiledb/broadcasts/
  - GET /companies/{company_key}/mobiledb/broadcasts
  - GET /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}
  - PUT /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}
  - DELETE /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}
  - GET /companies/{company_key}/mobiledb/subscription_lists/
  - GET /companies/{company_key}/sourcecodes
consequence: physical
human_in_the_loop: required
---

# Send a Vibes broadcast

Vibes publishes no `operationId` on any operation, so every step below names the operation as
`METHOD /path`. All calls are against `https://public-api.vibescm.com` (US) or
`https://public-api.eu.vibes.com/` (EU) — credentials are **not** portable between the two.

## Before every call

- `Authorization: Basic <base64(username:password)>`
- `Content-Type: application/json`
- `X-API-Version: 2` — **always send it**. Version 1 is the default and rejects E.164 numbers,
  so omitting the header silently gives you the version that cannot send internationally.

## Steps

1. **Pick the audience.** `GET /companies/{company_key}/mobiledb/subscription_lists/` and choose a
   `subscription_list_id`. There are no `page`/`page_size` parameters on this collection, so treat
   the response as the whole list.
2. **Pick the sender.** `GET /companies/{company_key}/sourcecodes` returns the active source/short
   codes the company may send from. The broadcast response echoes it as `source_short_code`.
3. **Create the broadcast.** `POST /companies/{company_key}/mobiledb/broadcasts/` with a
   `broadcastRequest` body. Note the trailing slash — the create path has one and the list path does
   not. Returns `200` or `201` with a `broadcastResponse` carrying `broadcast_id`.
   **There is no `Idempotency-Key` on this operation.** A timeout or a retry can create a second
   broadcast. Read back with step 4 before retrying, never retry blind.
4. **Confirm.** `GET /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}` and check the
   status field before assuming the send is queued.
5. **Amend if needed.** `PUT /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}`.
6. **Cancel while still scheduled.** `DELETE /companies/{company_key}/mobiledb/broadcasts/{broadcast_id}`.
   A `403` means the broadcast is no longer `scheduled` — it has already been sent and cannot be
   recalled.

## Errors you must branch on

| Status | Meaning | Action |
|---|---|---|
| 403 | Broadcast is not `scheduled` / already sent | Stop. Nothing is recoverable. Escalate to a human. |
| 404 | `broadcast_id` not found — **or** wrong `company_key` | Verify the tenant before assuming deletion. |
| 429 | Per-second throttle exceeded (100 req/s per `company_key`) | Back off. No `Retry-After` header is returned; choose your own schedule. |

The error body is **not** RFC 9457. It is `{"errors":[{"message":"...","code":N}]}` — an array,
so iterate. Vibes publishes no table mapping the numeric `code` to a meaning; only the HTTP status
and the English `message` are actionable.

## Guardrail

This skill puts messages on real handsets and is not reversible after step 3 completes. Require
explicit human confirmation of list, source code and message body before calling step 3.
