# DevOps Lab — Todo App (Implementation)

This repository implements a simple Todo web application (Node.js + Express) together with DevOps artifacts used for the course submission: automated tests, basic observability, and CI configuration.

Quick links

- Product backlog: [product backlog.md](product%20backlog.md)
- Project overview: [PROJECT_OVERVIEW.md](PROJECT_OVERVIEW.md)
- Sprint docs: [README_SPRINT1.md](README_SPRINT1.md) • [README_SPRINT2.md](README_SPRINT2.md)
- Sprint reviews: [SPRINT1_REVIEW.md](SPRINT1_REVIEW.md) • [SPRINT2_REVIEW.md](SPRINT2_REVIEW.md)

Summary

- Runtime: Node.js (Express) application located in the `app/` folder.
- Data: MongoDB via Mongoose (model: `app/models/Todo.js`).
- Tests: Jest + Supertest under `app/test/`.
- Entrypoint: `app/server.js` (exports the Express `app` for tests; started with `node server.js`).

Quick start — local development

Prerequisites: Node.js (18+), npm, and a running MongoDB instance (or set `MONGO_URI` to your DB).

1. Install dependencies

```powershell
cd app
npm ci
```

2. Run lint and tests

```powershell
npm run lint
npm test
```

3. Start the app (development)

```powershell
npm run dev
# or production-style start
npm start
```

Environment variables

- `MONGO_URI` — MongoDB connection string. The server will skip connecting to MongoDB when `NODE_ENV` is set to `test` (tests use the exported `app`).
- `PORT` — optional port (defaults to 3000).

API (JSON)

Base path: `/api`

- `GET /api/todos` — list todos; supports query filters:
  - `completed=true|false`
  - `priority=low|medium|high`
  - `category=<string>`
- `POST /api/todos` — create a todo. Body fields:
  - `task` (required)
  - `completed` (boolean)
  - `priority` (low|medium|high)
  - `dueDate` (ISO date)
  - `category` (string)
- `PATCH /api/todos/:id` — partial update (supports `task` and `completed`).
- `DELETE /api/todos/:id` — delete by id.

Operability

- Health endpoint: `GET /health` — returns status and uptime.
- Logging: Winston configured in `app/config/logger.js`; request logging via `morgan` is wired to the logger.
- Tracing: OpenTelemetry init and a request-id middleware exist in `app/middleware/tracing.js`.

Project structure (key files)

- [app/server.js](app/server.js) — Express app, middleware, routes mounting
- [app/routes/api.js](app/routes/api.js) — JSON API routes
- [app/routes/front.js](app/routes/front.js) — frontend routes and EJS view
- [app/models/Todo.js](app/models/Todo.js) — Mongoose schema (fields: task, completed, priority, dueDate, category)
- [app/config/logger.js](app/config/logger.js) — Winston logger configuration
- [app/middleware/tracing.js](app/middleware/tracing.js) — request id + tracing helper
- [app/test/](app/test/) — Jest + Supertest tests (exercise API and health endpoints)

Notes

- The `app/package.json` scripts expose `start`, `dev`, `test`, and `lint`.
- Tests run with `NODE_ENV=test` so the DB connection in `server.js` is skipped during tests.


