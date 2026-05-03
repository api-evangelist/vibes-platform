# Vibes Platform

Vibes is a mobile engagement platform that provides APIs for SMS messaging, push notifications, RCS for Business, and mobile marketing campaigns. The platform supports broadcast messaging, event-triggered messages, acquisition workflows, subscription list management, wallet pass management, and callback notifications. Vibes is a Tier 1 provider with direct carrier connections to AT&T, Verizon, T-Mobile, and regional carriers in the US and Canada.

**URL:** [apis.yml](https://raw.githubusercontent.com/api-evangelist/vibes-platform/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
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
- **Modified:** 2026-05-03

## APIs

### Vibes Platform API

The primary API for broadcast messaging, acquisition campaigns, subscription list management, wallet passes, event-triggered messages, and callback registrations.

**Base URL:** `https://public-api.vibescm.com` (US) | `https://public-api.eu.vibes.com` (EU)
**Authentication:** HTTP Basic Auth
**Human URL:** [developer-platform.vibes.com](https://developer-platform.vibes.com/)

#### Properties

- [Documentation](https://developer-platform.vibes.com/reference/our-apis)
- [Broadcast API Reference](https://developer-platform.vibes.com/reference/broadcast-api-1)
- [Acquisition Campaign API Reference](https://developer-platform.vibes.com/reference/acquisition-campaign-api-1)
- [Subscription List API Reference](https://developer-platform.vibes.com/reference/subscription-list-api)
- [OpenAPI Spec](openapi/vibes-platform-openapi.yml)
- [Spectral Rules](rules/vibes-platform-rules.yml)

### Vibes Connect API

Aggregation-layer APIs for sending and receiving SMS and MMS messages directly via HTTP. Includes the HTTP Message API (SMS), SMPP Gateway API, and MMS Message API (MM7 Protocol).

**Base URL:** `https://messageapi.vibesapps.com` (SMS) | `https://messageapi-mms.vibesapps.com` (MMS)
**Authentication:** HTTP Basic Auth
**Human URL:** [developer-aggregation.vibes.com](https://developer-aggregation.vibes.com)

#### Properties

- [Documentation](https://developer-aggregation.vibes.com)
- [HTTP Message API Reference](https://developer-aggregation.vibes.com/reference/http-message-api)
- [OpenAPI Spec](openapi/vibes-connect-openapi.yml)

## OpenAPI Specifications

| File | Description |
|---|---|
| [vibes-platform-openapi.yml](openapi/vibes-platform-openapi.yml) | Vibes Platform API (broadcasts, campaigns, subscriptions, events, wallet passes, callbacks) |
| [vibes-connect-openapi.yml](openapi/vibes-connect-openapi.yml) | Vibes Connect API (SMS, MMS, carrier lookup) |

## Spectral Rules

| File | Description |
|---|---|
| [vibes-platform-rules.yml](rules/vibes-platform-rules.yml) | Spectral ruleset enforcing Vibes API conventions |

## Naftiko Capabilities

### Workflow Capabilities

| File | Description |
|---|---|
| [capabilities/mobile-messaging.yaml](capabilities/mobile-messaging.yaml) | Unified mobile messaging workflow combining Platform API and Connect API (16 tools) |

### Shared Per-API Definitions

| File | Description |
|---|---|
| [capabilities/shared/vibes-platform.yaml](capabilities/shared/vibes-platform.yaml) | Vibes Platform API shared capability definition |
| [capabilities/shared/vibes-connect.yaml](capabilities/shared/vibes-connect.yaml) | Vibes Connect API shared capability definition |

## JSON Schema

| File | Description |
|---|---|
| [json-schema/vibes-platform-broadcast-schema.json](json-schema/vibes-platform-broadcast-schema.json) | Broadcast resource schema |
| [json-schema/vibes-platform-person-schema.json](json-schema/vibes-platform-person-schema.json) | Person (subscriber) resource schema |
| [json-schema/vibes-platform-subscription-list-schema.json](json-schema/vibes-platform-subscription-list-schema.json) | Subscription list resource schema |

## JSON Structure

| File | Description |
|---|---|
| [json-structure/vibes-platform-broadcast-structure.json](json-structure/vibes-platform-broadcast-structure.json) | Broadcast resource field documentation |

## JSON-LD

| File | Description |
|---|---|
| [json-ld/vibes-platform-context.jsonld](json-ld/vibes-platform-context.jsonld) | JSON-LD context mapping Vibes vocabulary to schema.org |

## Examples

| File | Description |
|---|---|
| [examples/vibes-platform-listBroadcasts-example.json](examples/vibes-platform-listBroadcasts-example.json) | List broadcasts request/response example |
| [examples/vibes-platform-createBroadcast-example.json](examples/vibes-platform-createBroadcast-example.json) | Create broadcast request/response example |
| [examples/vibes-platform-addParticipant-example.json](examples/vibes-platform-addParticipant-example.json) | Add participant to acquisition campaign example |
| [examples/vibes-platform-createEvent-example.json](examples/vibes-platform-createEvent-example.json) | Create event-triggered message example |
| [examples/vibes-connect-sendSmsMessage-example.json](examples/vibes-connect-sendSmsMessage-example.json) | Send SMS message via Connect API example |

## Vocabulary

| File | Description |
|---|---|
| [vocabulary/vibes-platform-vocabulary.yml](vocabulary/vibes-platform-vocabulary.yml) | Vibes Platform domain vocabulary and taxonomy |

## Developer Portals

- [Vibes Platform Developer Portal](https://developer-platform.vibes.com/)
- [Vibes Connect Developer Portal](https://developer-aggregation.vibes.com)
- [Vibes RCS for Business Portal](https://developer-rbm.vibes.com/)
- [Vibes Website](https://www.vibes.com/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
