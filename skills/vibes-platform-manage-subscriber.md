---
name: vibes-platform-manage-subscriber
description: >-
  Look up, create and update a person in the Vibes MobileDB, read their subscriptions, and
  unsubscribe them — using either the Vibes person_key or your own external_person_id.
generated: '2026-08-13'
method: generated
source: openapi/vibes-platform-api-openapi.json, https://developer-platform.vibes.com/reference/person-api
api: Vibes Platform API
base_url: https://public-api.vibescm.com
operations:
  - GET /companies/{company_key}/mobiledb/persons
  - GET /companies/{company_key}/mobiledb/persons/{person_key}
  - GET /companies/{company_key}/mobiledb/persons/external/{external_person_id}
  - POST /companies/{company_key}/mobiledb/persons/
  - PUT /companies/{company_key}/mobiledb/persons/{person_key}
  - PUT /companies/{company_key}/mobiledb/persons/external/{external_person_id}
  - GET /companies/{company_key}/mobiledb/persons/{person_key}/subscriptions
  - GET /companies/{company_key}/mobiledb/persons/{person_key}/subscriptions/{subscription_list_id}
  - DELETE /companies/{company_key}/mobiledb/persons/{person_key}/subscriptions/{subscription_list_id}
  - DELETE /companies/{company_key}/mobiledb/persons/external/{external_person_id}/subscriptions/{subscription_list_id}
consequence: write
human_in_the_loop: recommended
---

# Manage a Vibes subscriber

Every Person route exists twice: once keyed by the Vibes `person_key`, once by your own
`external_person_id`. Use the `external/` variants if your CRM is the system of record — you then
never have to persist a Vibes identifier.

Headers on every call: `Authorization: Basic …`, `Content-Type: application/json`,
`X-API-Version: 2`.

## Find

- By phone number: `GET /companies/{company_key}/mobiledb/persons?mdn=+12025550132`.
  **URL-encode the leading `+` as `%2B`** — Vibes says so explicitly and returns `400`
  *"Invalid MDN format"* otherwise.
- By Vibes key: `GET /companies/{company_key}/mobiledb/persons/{person_key}`.
- By your key: `GET /companies/{company_key}/mobiledb/persons/external/{external_person_id}`.

## Create

`POST /companies/{company_key}/mobiledb/persons/` with a `personRequest`. A `409` means the MDN is
already associated with another person record — that is a match, not a failure. Resolve by looking
the person up rather than retrying.

## Update

`PUT .../persons/{person_key}` or `PUT .../persons/external/{external_person_id}`.

**The MDN is immutable.** Attempting to change it returns `409`. Vibes' documented workaround is to
remove the number, not to update it. Do not build a retry loop around this status.

## Subscriptions

- All lists for a person: `GET .../persons/{person_key}/subscriptions`
- Status on one list: `GET .../persons/{person_key}/subscriptions/{subscription_list_id}`
- Unsubscribe: `DELETE .../persons/{person_key}/subscriptions/{subscription_list_id}`

A `404` on unsubscribe means *either* the person was not found *or* they were already not subscribed
— Vibes returns the same status for both, so treat it as success-or-absent, never as an error to
retry.

## Privacy

Consumer Privacy Act requests and CPR nullification of MobileDB records are a separate documented
flow (`https://developer-platform.vibes.com/docs/cpr-nullification-of-mobiledb-records`). Do not
attempt to satisfy an erasure request by calling `PUT` on the person record.

## Errors

Body shape is `{"errors":[{"message":"…","code":N}]}` — an array, not RFC 9457. Throttle is
100 req/s per `company_key`; `429` carries no `Retry-After`.
