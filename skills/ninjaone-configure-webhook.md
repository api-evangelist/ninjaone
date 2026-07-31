---
name: Configure activity webhooks
description: Register or remove the NinjaOne activity-notification webhook so events are pushed to a callback URL.
api: openapi/ninjaone-openapi-original.yml
operations: [configureWebhook, disableWebhook]
---

# Configure activity webhooks (NinjaOne)

Requires the `management` OAuth scope.

## Auth
OAuth 2.0 Bearer token with `scope=management`.

## Steps
1. `configureWebhook` (PUT `/v2/webhook`) — set the `WebhookConfiguration`:
   - `url`: your HTTPS callback endpoint.
   - `activities`: a filter map selecting which activity classes/types to receive.
   - `expand`: which references to expand inline in delivered payloads.
   - `headers`: custom headers NinjaOne adds to each callback (use for verification).
2. NinjaOne POSTs activity notifications to `url` as matching activities occur.
3. `disableWebhook` (DELETE `/v2/webhook`) — remove the configuration.

## Rules
- One webhook configuration per tenant; `configureWebhook` replaces it.
- Verify inbound deliveries using the custom `headers` you set.
- See `asyncapi/ninjaone-webhooks.yml` for the event/delivery model.
