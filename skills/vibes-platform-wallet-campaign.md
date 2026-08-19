---
name: vibes-platform-wallet-campaign
description: >-
  Stand up a Vibes mobile wallet campaign end to end — create the campaign, author the Apple and
  Google pass templates, attach store locations idempotently, publish the Add-to-Wallet landing
  page, and message pass holders.
generated: '2026-08-13'
method: generated
source: >-
  openapi/vibes-platform-api-openapi.json,
  https://developer-platform.vibes.com/reference/wallet-campaign-api
api: Vibes Platform API
base_url: https://public-api.vibescm.com
operations:
  - POST /companies/{company_key}/campaigns/wallet
  - GET /companies/{company_key}/campaigns/wallet
  - GET /companies/{company_key}/campaigns/wallet/{wallet_id}
  - PUT /companies/{company_key}/campaigns/wallet/{wallet_id}
  - POST /companies/{company_key}/campaigns/wallet/{token}/passbook_template
  - PUT /companies/{company_key}/campaigns/wallet/{token}/passbook_template
  - POST /companies/{company_key}/campaigns/wallet/{token}/wallet_template
  - PUT /companies/{company_key}/campaigns/wallet/{token}/wallet_template
  - POST /companies/{company_key}/campaigns/wallet/{token}/locations/bulk
  - GET /companies/{company_key}/campaigns/wallet/{token}/locations
  - DELETE /companies/{company_key}/campaigns/wallet/{token}/locations/{id}
  - DELETE /companies/{company_key}/campaigns/wallet/{token}/locations/delete_all
  - POST /companies/{company_key}/campaigns/wallet/{token}/location_selector
  - GET /companies/{company_key}/campaigns/wallet/{wallet_id}/items
  - POST /companies/{company_key}/campaigns/wallet/{wallet_id}/messages
consequence: physical
human_in_the_loop: required
---

# Build a Vibes wallet campaign

## The identifier trap — read this first

A wallet campaign is addressed **two different ways in the same published spec**:

- `{wallet_id}` on the campaign itself, its items and its messages
- `{token}` on the pass templates, the store locations and the location selector

They are not interchangeable in the paths even though they name the same campaign. Carry both.

## Steps

1. **Create the campaign.** `POST /companies/{company_key}/campaigns/wallet`.
   `type` is one of `offer`, `loyalty`, `event_ticket` and is **immutable after creation** —
   Vibes says so explicitly. Getting it wrong means creating a new campaign, not fixing this one.
2. **Author the Apple template.** `POST .../campaigns/wallet/{token}/passbook_template`. Field
   semantics follow Apple Wallet Passes (PassKit). One template per campaign — `POST` to create,
   `PUT` to update.
3. **Author the Google template.** `POST .../campaigns/wallet/{token}/wallet_template`. Field
   semantics follow Google Wallet generic passes. Also one per campaign.
   Many text fields in both templates accept **Liquid** personalization tags resolved per recipient
   (`https://developer-platform.vibes.com/docs/using-liquid-language-template`).
4. **Attach store locations.** `POST .../campaigns/wallet/{token}/locations/bulk`, up to **1000 per
   call**.
   **`Idempotency-Key` is REQUIRED on this operation** — it is the only operation in the entire
   75-operation API that takes one. Repeating a request with the same key returns the original
   result without inserting duplicates. Generate one key per logical batch and reuse it on retry;
   do not generate a fresh key when retrying a timeout.
   Read back with `GET .../locations` (this is also the only endpoint with `page` / `page_size`).
   Remove with `DELETE .../locations/{id}` or, filtered/whole, `DELETE .../locations/delete_all`.
5. **Publish the landing page.** `POST .../campaigns/wallet/{token}/location_selector` creates the
   branded "Add to Wallet" page. `GET`/`PUT`/`DELETE` manage it.
6. **Watch adoption.** `GET .../campaigns/wallet/{wallet_id}/items` lists the per-recipient passes.
   Installs and removals also arrive as callbacks — `wallet_item_install` and `wallet_item_remove`
   (see `skills/vibes-platform-register-callbacks.md`).
7. **Message holders.** `POST .../campaigns/wallet/{wallet_id}/messages`, optionally filtered by
   token value or group code.
   **This reaches real devices. Confirm with a human first.** There is no idempotency key on this
   operation.

## Throttle

Google Wallet updates are limited to **20 requests/second** — five times tighter than the general
100 req/s limit and the binding constraint on any bulk template or location work. `429` carries no
`Retry-After`.
