---
name: vibes-platform-register-callbacks
description: >-
  Register, test, inspect and cancel Vibes callbacks (webhooks) so your system receives opt-in,
  opt-out, person, push-device and wallet events.
generated: '2026-08-13'
method: generated
source: >-
  openapi/vibes-platform-api-openapi.json,
  https://developer-platform.vibes.com/reference/callbacks,
  asyncapi/vibes-platform-webhooks.yml
api: Vibes Platform API
base_url: https://public-api.vibescm.com
operations:
  - POST /companies/{company_key}/config/callbacks/
  - GET /companies/{company_key}/config/callbacks/
  - GET /companies/{company_key}/config/callbacks/{callback_id}
  - PUT /companies/{company_key}/config/callbacks/{callback_id}
  - DELETE /companies/{company_key}/config/callbacks/{callback_id}
  - POST /companies/{company_key}/config/callback_events/test
consequence: write
human_in_the_loop: optional
---

# Register Vibes callbacks

Vibes calls its webhooks **callbacks**. There are 20 published event types across eight groups;
`asyncapi/vibes-platform-webhooks.yml` in this repo is the full catalog.

## Rules that will bite you

- **One registration per callback type, per company.** You cannot register `person_added` twice for
  the same company. Person callbacks are keyed to the whole mobile database, not the company.
- To fan out to more than one destination, register the same callback type again with a different
  destination URL. **Maximum 50 endpoint URLs.**
- **No signature.** Vibes publishes no HMAC, shared secret or signing header. The only integrity
  control offered is source-IP allowlisting.
- **At-least-once delivery.** Vibes states an event may arrive more than once. Your handler must be
  idempotent on the event body.

## Steps

1. **Register.** `POST /companies/{company_key}/config/callbacks/` with the request body for the
   type you want — the spec models one per group: `callbackRequest-Ack`, `-Event`, `-Person`,
   `-Push`, `-Sub`, `-SubList`, `-Unmatched`, `-Wallet`. Returns `callback_id`.
2. **Fire a test event.** `POST /companies/{company_key}/config/callback_events/test` with the
   matching `testcallbackRequest-*` body. Use this before you go live — it is the only way to
   exercise your handler without waiting for real subscriber activity.
3. **List / read.** `GET /companies/{company_key}/config/callbacks/` and
   `GET /companies/{company_key}/config/callbacks/{callback_id}`.
4. **Update or cancel.** `PUT` / `DELETE` on `{callback_id}`.

## What your endpoint must return

| You return | Vibes does |
|---|---|
| 2XX | Accepts the event. Done. |
| 4XX | **Permanent failure — no retry.** Event goes straight to the failure queue and the customer is notified. |
| 3XX or 5XX | Transient. Retried on the configured scheme, then queued as a failure. Repeated failures can mark your URL "downed" and suspend delivery for a period. |

Return `2XX` whenever you have durably accepted the event, even if downstream processing has not
finished. Keep the handler small — Vibes warns that slow handlers trigger rate limiting and
timeouts. Do the real work asynchronously.

## Allowlist Vibes' egress

Routing metadata arrives in the HTTP **headers**; the body carries only event-specific data.
Callbacks originate from published fixed IPs:

- **US:** 35.155.139.143, 52.32.61.199, 35.161.244.84, 18.205.120.48, 52.22.43.57, 18.232.9.131
- **EU:** 34.243.232.57, 52.48.241.82, 34.249.188.130, 54.247.36.51, 34.253.250.65, 54.217.181.160

Since there is no signature, this allowlist is your only authenticity check. Treat an unsigned
callback from an unlisted IP as hostile.
