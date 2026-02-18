# Sprint 2 — Review

## What was delivered

- Observability: `morgan` request logging forwarded to `winston` and structured log formatting.
- Robustness: centralized error middleware and input validation for `POST /` with `express-validator`.
- Operability: `/health` endpoint returning service status and uptime.
- CI: ESLint integrated into the CI pipeline; pipeline fails on lint or test failures.

## Acceptance Evidence

- CI workflow file: [.github/workflows/ci.yml](.github/workflows/ci.yml)
- Tests: see `app/test/` (unit & integration tests). Key files: `app/test/api.test.js`, `app/test/todos.test.js`.
- Health endpoint sample: `GET /health` returns `{ "status": "ok", "uptime": ... }`.
- Logs: example request-level logs visible when running locally or in the container (see `app/config/logger.js`).

## Demonstration notes

- Start the app: `cd app && npm ci && npm run dev` and open `/health`.
- Run lint and tests: `npm run lint` then `npm test`.
- CI: check the Actions tab for runs against `develop` and `main` (workflow: `.github/workflows/ci.yml`).

## Next steps

- Add automated screenshot/log capture for submission (put artifacts under `/screenshots/`).
- Add monitoring integration for production (e.g., Sentry or Datadog) and persistent log aggregation.
