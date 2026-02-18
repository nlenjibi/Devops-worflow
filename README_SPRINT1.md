# Sprint 1 — Execution Summary

## Sprint Goal

Deliver a stable CRUD increment for the Todo REST prototype: create, list, update (mark complete). Provide automated tests and CI to demonstrate delivery discipline.

## Delivered Work

- Frontend (HTML) routes: `GET /` (render list), `POST /` (create via form), and `POST /todo/destroy` (delete form action).
- JSON API: `/api/todos` endpoints (GET, POST, PATCH, DELETE) for programmatic access.
- Project structure: Express routes and `models/Todo` (Mongoose).
- Tests: Jest + Supertest tests added at `app/test/front.test.js` (mocked model where appropriate) and `app/test/api.test.js` for API flows.
- CI: GitHub Actions workflow added at `.github/workflows/ci.yml` to run tests on `develop` and `main`.

## How to run locally

From repository root:

```powershell
cd app
npm install
npm test
npm run dev   # to run with nodemon
```

Notes: See `app/test/` for concrete examples of expected behavior and test coverage.
