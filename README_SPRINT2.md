# Sprint 2 — Execution Summary

## Sprint Goal

Implement observability and robustness improvements: structured logging, centralized error handling, health endpoint, and input validation. Add basic linting to CI.

## Delivered Work

- Structured logging via `winston` and request logging via `morgan`.
- Centralized error handler returning JSON for API consumers and simple HTML for browser requests.
- `/health` endpoint implemented for operability checks.
- Request validation added to both the frontend `POST /` form handler and the JSON API `POST /api/todos` using `express-validator`.
- Linting integrated into CI with ESLint.

## How to run locally

From repository root:

```powershell
cd app
npm install
npm run lint
npm test
npm run dev
```
