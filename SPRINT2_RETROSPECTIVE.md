# Sprint 2 — Retrospective

## What went well

- Added structured logging and health checks quickly; CI now enforces lint and tests.
- Centralized error handling improved testability and consistency.

## What didn't go well

- Adding linting surfaced style issues; some small tweaks required to pass CI.
- The HTML-rendering routes and API-style error JSON required dual-format error responses.

## Actionable improvements for future work

1. Add correlation IDs to logs and persist logs to a file or external system (measurable by presence of correlation ID in log entries).
2. Introduce feature flags and environment-specific configurations (measurable by a config file and documented feature-flag toggles).
