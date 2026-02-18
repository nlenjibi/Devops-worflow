

# DevOps Todo App — Project Documentation

## Table of Contents

- Executive Summary
- Architecture & Components
- Technology Stack
- Getting Started (Local)
- Environment Variables
- Running the App
- Tests
- API Reference
- Data Model
- Frontend
- Observability
- CI / GitHub Actions
- Deployment
- Project Structure
- User Stories (summary)
- Known Limitations & Next Steps
- Contact

---

## Executive Summary

This repository contains a Node.js + Express Todo web application intended for demonstrating Agile & DevOps practices: automated testing, structured logging, tracing, containerization guidance, and CI. It exposes both a simple HTML frontend (EJS) and a JSON REST API backed by MongoDB.

The implementation focuses on a small, testable codebase with clear separation of concerns, enabling automated tests and CI to validate core behaviors.

---

## Architecture & Components

- Express application (`app/server.js`) that mounts frontend and API routers.
- MongoDB via Mongoose for persistence (`app/models/Todo.js`).
- Frontend: EJS templates under `app/views/` for a minimal UI.
- Observability: Winston logger (`app/config/logger.js`) and request logging via `morgan`; OpenTelemetry tracing initialized in middleware (`app/middleware/tracing.js`).
- Tests: Jest + Supertest for unit & integration tests in `app/test/`.

---

## Technology Stack

- Node.js (tested on Node 18+)
- Express
- MongoDB + Mongoose
- EJS templates for server-rendered frontend
- OpenTelemetry, Winston, Morgan for observability
- Jest + Supertest for testing
- ESLint for linting

---

## Getting Started (Local)

Prerequisites: Node.js 18+, npm, and a MongoDB instance (local or remote).

1. Install dependencies

```powershell
cd app
npm ci
```

2. Copy environment variables

Create a `.env` file in `app/` or set `MONGO_URI` and `PORT` in your environment. Example (not for production):

```text
MONGO_URI=mongodb://root:root@localhost:27017/todoapp?authSource=admin
PORT=3000
```

3. Run the app (development)

```powershell
npm run dev
# or
npm start
```

The app listens by default on `http://localhost:3000`.

---

## Environment Variables

- `MONGO_URI` — MongoDB connection string (required in non-test env).
- `PORT` — server port (optional; default 3000).
- `NODE_ENV` — set to `test` when running tests to avoid automatic DB connect in `server.js`.

---

## Running Tests

From the `app/` folder:

```powershell
npm test
```

Notes:

- `app/test/` includes both DB-backed integration tests and mocked tests. Some integration tests require a running MongoDB instance.
- Front-route tests mock the `Todo` model to avoid requiring a DB.

---

## API Reference

Base path: `/api`

- `GET /api/todos` — List todos. Query params supported:
  - `completed=true|false`
  - `priority=low|medium|high`
  - `category=<string>`

- `POST /api/todos` — Create a todo. JSON body fields:
  - `task` (string, required)
  - `completed` (boolean)
  - `priority` (low|medium|high)
  - `dueDate` (ISO date)
  - `category` (string)

- `PATCH /api/todos/:id` — Update todo (currently supports `task` and `completed` fields).

- `DELETE /api/todos/:id` — Delete a todo by id.

Operability endpoint:

- `GET /health` — Returns `{ status: 'ok', uptime: <seconds> }`.

---

## Data Model

`app/models/Todo.js` defines the schema:

- `task`: String (required)
- `completed`: Boolean (default: false)
- `priority`: String enum [`low`,`medium`,`high`] (default: `medium`)
- `dueDate`: Date | null
- `category`: String | null
- `created_at`: Date (default: now)

Note: the model is exported as `mongoose.model('todos', TodoSchema)`.

---

## Frontend

The server-rendered UI is a minimal EJS template at `app/views/todos.ejs` with the following behavior:

- `GET /` renders the todo list (reads all todos).
- `POST /` accepts form submissions to create a new todo (`task` field) and redirects back to `/`.
- Deletion is implemented as a form POST to `/todo/destroy` with hidden `_key` field; the route removes the todo and redirects to `/`.

Limitations:

- The UI does not currently provide an in-page toggle to change completion status.
- There is no client-side confirmation modal for deletion in the current template.

---

## Observability

- Winston: central logger configured in `app/config/logger.js`.
- Morgan: HTTP request logging integrated and piped to Winston.
- OpenTelemetry: basic tracing middleware is present in `app/middleware/tracing.js` and is initialized early in `server.js`.
- Request ID: middleware sets and exposes `req.id` and `X-Request-Id` header for correlating logs and traces.

---

## CI / GitHub Actions

CI workflow is expected at `.github/workflows/ci.yml` (runs lint and tests). The intended pipeline steps:

- checkout
- install dependencies
- start a MongoDB service for integration tests (where applicable)
- run `npm run lint`
- run `npm test`

Ensure CI sets `NODE_ENV=test` where appropriate so `server.js` skips automatic DB connect.

---

## Deployment

Two deployment approaches are documented:

- Vercel (serverless Node.js): requires configuring `MONGO_URI` in Vercel environment settings. Note serverless cold-starts and connection pooling considerations.
- Docker: repository contains Docker/compose artifacts (if present) to run app + MongoDB together for consistent deployments.

---

## Project Structure (key files)

- `app/server.js` — Express app and middleware
- `app/routes/api.js` — JSON API routes
- `app/routes/front.js` — frontend routes
- `app/models/Todo.js` — Mongoose model
- `app/views/todos.ejs` — HTML template
- `app/config/logger.js` — logging setup
- `app/middleware/tracing.js` — tracing / request-id middleware
- `app/test/` — Jest + Supertest tests
- `app/package.json` — scripts and dependencies

---

## User Stories (summary)

Key delivered user stories (implementation status):

- Basic todo creation (web form + `POST /api/todos`) — implemented and tested.
- Todo listing (`GET /` and `GET /api/todos`) — implemented and tested.
- Deletion (frontend `POST /todo/destroy`, API `DELETE /api/todos/:id`) — implemented.
- Priority, due date, category fields — model and `POST /api/todos` support them; `PATCH` only updates `task` and `completed` at present.
- Health endpoint, logging, and tracing — implemented; covered by tests.

---

## Known Limitations & Next Steps

- UI improvements: add completion toggle, deletion confirmation, and inputs for `priority`, `dueDate`, and `category`.
- Extend `PATCH /api/todos/:id` to accept updates for `priority`, `dueDate`, and `category`.
- Add full-text search and date-range filtering to the API.
- Secure production MongoDB credentials and remove `root:root` example credentials.
- Consider connection pooling or an adapter for serverless deployments (Vercel).

---

## Contact

Project owner: Timothy Nlenjibi

---

Generated from repository state on 2026-02-18.
