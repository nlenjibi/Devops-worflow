# Sprint 1 — Retrospective

## What went well

- Core features already existed enabling quick alignment to Sprint goals.
- Added automated tests and CI to demonstrate delivery discipline.

## What didn't go well

- Original server started automatically and forced DB connection, which hindered testability.
- No `test` script or test tooling originally present.

## Actionable improvements for Sprint 2

1. Add centralized logging (Winston) and request-level correlation IDs — measurable by presence of structured logs for requests.
2. Implement centralized error-handling middleware and a `/health` endpoint — measurable by new endpoint returning 200 and standardized error payloads.
