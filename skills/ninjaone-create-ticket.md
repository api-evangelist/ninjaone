---
name: Create and comment on a helpdesk ticket
description: Open a NinjaOne helpdesk ticket for a device/organization and add a comment.
api: openapi/ninjaone-openapi-original.yml
operations: [create, getTicketById, createComment]
---

# Create and comment on a ticket (NinjaOne)

Requires the `management` OAuth scope.

## Auth
Obtain an OAuth 2.0 Bearer token with `scope=management` (client-credentials or
authorization-code). Send `Authorization: Bearer <token>`.

## Steps
1. `create` — create a ticket (NewTicket body: subject, description, and optional
   `locationId` / `nodeId` to associate it with a location/device).
2. `getTicketById` — read the created ticket back by id to confirm state.
3. `createComment` — add a comment/log entry to the ticket.

## Rules
- Ticket bodies reference `locationId` and `nodeId` (device) — resolve these first
  via the inventory skill.
- No idempotency-key is supported; avoid duplicate `create` calls
  (see `conventions/ninjaone-conventions.yml`).
- On `403`, the token lacks the `management` scope.
