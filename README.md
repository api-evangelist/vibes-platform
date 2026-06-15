# Vibes Platform (vibes-platform)

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
