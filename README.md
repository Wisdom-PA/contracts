# Contracts – API shapes (cube ↔ app)

API definitions shared by the cube and the mobile app: REST shapes, request/response schemas. Optionally app ↔ backend.

- **Format:** OpenAPI 3.0 (YAML). Cube and app consume this repo (submodule, npm package, or CI copy).
- **Plan and tickets:** See Wisdom root (Plan.md, GettingStarted.md, Tickets.md).

## Cube ↔ App API

- **Spec:** `openapi/cube-app.yaml` — status, config, devices, routines, profiles, logs, backup/restore.
- **Base URL:** Over LAN (e.g. `http://cube.local`) or tunnel after Bluetooth pairing; replace host/port in app as needed.

## Consumption

| Consumer | How |
| -------- | --- |
| **Cube** | Read the spec; implement endpoints in the API gateway. No codegen required; keep implementation in sync with schemas. |
| **App** | Option A — copy or submodule this repo; generate TypeScript types or a client (e.g. `openapi-typescript`, `openapi-generator-cli`). Option B — CI job that publishes an npm package with types. |
| **Tests** | App integration tests can stub responses using the same schemas; cube tests mock the gateway. |

Validate the spec (e.g. `npx @redocly/cli lint openapi/cube-app.yaml` or any OpenAPI validator) in CI when the contracts repo is updated.
