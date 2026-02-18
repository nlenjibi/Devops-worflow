# Sprint 2 — Improvements, CI/CD, Deployment & Delivery Checklist

## Summary of Sprint 2 Improvements

- Structured logging via `winston` and request logging with `morgan`.
- Centralized error handler in `server.js` for consistent HTTP responses.
- Health endpoint: `GET /health` returning `{"status":"ok","uptime":...}`.
- Input validation using `express-validator` for user inputs.
- Extended `Todo` model with `priority`, `dueDate`, and `category` fields.
- JSON API endpoints at `/api/todos` supporting query filtering. The app also exposes frontend routes (`/`, `/todo/destroy`) which render and accept form submissions.
- Integration tests added: `app/test/api.test.js`, `app/test/todos.test.js`.
- ESLint added and enforced in CI (`.github/workflows/ci.yml`).

## How to run locally (development)

1. Create `.env` from `.env.example` and set `MONGO_URI`.

3. From project root, run server:

```powershell
cd app
npm ci
npm run dev
```

4. Run tests (requires accessible MongoDB):

```powershell
cd app
npm test --runInBand
```

## CI / GitHub Actions

- Workflow: `.github/workflows/ci.yml` (runs on push/PR to `develop` and `main`).
- Steps: checkout, install, wait for MongoDB service, lint (build fails on lint errors), run Jest tests (build fails on test failures).
- The CI workflow config lives at [.github/workflows/ci.yml](.github/workflows/ci.yml).

## Vercel Deployment

1. Connect the GitHub repository to Vercel.
2. Add environment variable `MONGO_URI` in Vercel Project Settings (Production/Preview/Development).

   Key: `MONGO_URI`

   Example value: `mongodb+srv://root:<password>@cluster0.rr0muys.mongodb.net/todo_db?retryWrites=true&w=majority`

3. `vercel.json` is included to configure serverless settings. After merge to `main`, Vercel deploys automatically — verify `/health`.

## Branching & Protection Recommendations

- Branch model: `main` (production), `develop`, `feature/*`.
- Protect `main` and `develop`: require PR reviews and CI status checks (lint + tests) to pass before merge.

## Definition of Done (Sprint & Submission)

- Code merged via PR with passing CI (lint + tests).
- Tests covering core API behavior present under `app/test/`.
- README and sprint artifacts included for evaluation.

## Checklist (Final Deliverables)

- [ ] Product backlog & sprint plans (Sprint 0, 1, 2) — see [product backlog.md](product%20backlog.md)
- [x] Sprint 1 implementation (CRUD + MongoDB)
- [x] CI workflow [.github/workflows/ci.yml](.github/workflows/ci.yml)
- [x] Jest tests in `app/test/`
- [x] ESLint config and linting in CI
- [x] `vercel.json` and Vercel deployment instructions
- [x] `.env.example` showing `MONGO_URI`
- [x] Sprint Reviews & Retrospectives

## Next recommended steps

- Configure Vercel env vars and deploy to Preview/Production.
- Add monitoring/alerting (Sentry, Datadog) and persistent log aggregation.
- Harden MongoDB credentials for production (avoid root/root; use restricted user and network rules).
