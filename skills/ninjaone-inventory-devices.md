---
name: Inventory organizations and devices
description: Authenticate to the NinjaOne Public API and enumerate organizations and their managed devices, including active alerts.
api: openapi/ninjaone-openapi-original.yml
operations: [getOrganizations, getOrganization, getOrganizationDevices, getDevice, getDeviceAlerts]
---

# Inventory organizations and devices (NinjaOne)

Read-only endpoint discovery of the NinjaOne estate. Requires the `monitoring` OAuth scope.

## Auth
1. Obtain an OAuth 2.0 Bearer token via client-credentials from
   `https://app.ninjarmm.com/ws/oauth/token` with `scope=monitoring`
   (see `authentication/ninjaone-authentication.yml`). Tokens expire in 3600s.
2. Send `Authorization: Bearer <token>` on every request. Use the API host for
   your tenant region (e.g. `https://app.ninjarmm.com/v2`).

## Steps
1. `getOrganizations` — list all organizations (clients). Page with `pageSize` + `cursor`.
2. `getOrganization` — fetch a single organization for detail.
3. `getOrganizationDevices` — list the devices belonging to an organization.
4. `getDevice` — fetch full device detail by id.
5. `getDeviceAlerts` — list active alerts/conditions for a device.

## Rules
- Pagination is cursor-based (`cursor` + `pageSize`); follow the returned cursor.
- Honor `429` rate-limit responses with backoff (see `conventions/ninjaone-conventions.yml`).
- Errors are bare HTTP statuses (401 token, 403 scope, 404 not found) — see `errors/ninjaone-problem-types.yml`.
