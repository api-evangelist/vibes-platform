# Vibes Platform (vibes-platform)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Vibes is a mobile engagement platform that provides APIs for SMS messaging, push notifications, RCS for Business, and mobile marketing campaigns. The platform APIs support broadcast messaging, event-triggered messages, acquisition workflows, subscription list management, wallet pass management, and callback notifications for opt-ins and delivery status. Vibes operates as a Tier 1 provider with direct carrier connections in the US and Canada.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/apis.yml)

## Scope

- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Mobile Marketing
- Mobile Messaging
- Push Notifications
- SMS
- MMS
- Broadcast Messaging
- Acquisition Campaigns
- Subscription Management
- Wallet Passes
- RCS

## Timestamps

- **Created:** 2024-11-14
- **Modified:** 2026-05-19

## APIs

### Vibes Platform API

The Vibes Platform API provides programmatic access to broadcast messaging (SMS and push notifications), acquisition workflows, subscription list management, wallet pass management, and event-triggered message capabilities. Broadcasts are delivered to subscribers within your mobile contact book. Authentication uses HTTP Basic Auth with Base64-encoded credentials. The US environment base URL is https://public-api.vibescm.com and the EU environment base URL is https://public-api.eu.vibes.com.

- **Human URL:** [https://developer-platform.vibes.com/](https://developer-platform.vibes.com/)
- **Base URL:** `https://public-api.vibescm.com`

#### Tags

- Mobile Marketing
- Push Notifications
- SMS
- Broadcast
- Acquisition
- Subscription Management
- Wallet Passes

#### Properties

- [Documentation](https://developer-platform.vibes.com/reference/our-apis)
- [Reference](https://developer-platform.vibes.com/reference/broadcast-api-1)
- [Reference](https://developer-platform.vibes.com/reference/acquisition-campaign-api-1)
- [Reference](https://developer-platform.vibes.com/reference/subscription-list-api)
- [Reference](https://developer-platform.vibes.com/reference/callbacks)
- [Reference](https://developer-platform.vibes.com/reference/technical-details)
- [OpenAPI](openapi/vibes-platform-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/vibes-platform.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/vibes-platform.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Spectral Ruleset](rules/vibes-platform-rules.yml)

### Vibes Connect API

Vibes Connect provides aggregation-layer APIs for sending and receiving SMS and MMS messages via HTTP calls. Three APIs are offered: the HTTP Message API for SMS, the SMPP Gateway API for persistent SMPP bindings, and the MMS Message API using MM7 Protocol. Vibes is a Tier 1 provider with direct connections to Verizon, AT&T, T-Mobile, and regional carriers. US SMS endpoint: https://messageapi.vibesapps.com; US MMS endpoint: https://messageapi-mms.vibesapps.com.

- **Human URL:** [https://developer-aggregation.vibes.com](https://developer-aggregation.vibes.com)
- **Base URL:** `https://messageapi.vibesapps.com`

#### Tags

- SMS
- MMS
- Aggregation
- Messaging
- Mobile

#### Properties

- [Documentation](https://developer-aggregation.vibes.com)
- [Reference](https://developer-aggregation.vibes.com/reference/http-message-api)
- [OpenAPI](openapi/vibes-connect-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/vibes-connect.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/vibes-connect.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Portal](https://developer-platform.vibes.com/)
- [Documentation](https://developer-platform.vibes.com/reference/our-apis)
- [Portal](https://developer-aggregation.vibes.com)
- [Portal](https://developer-rbm.vibes.com/)
- [Website](https://www.vibes.com/)
- [Integrations](https://www.vibes.com/platform/integrations)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
