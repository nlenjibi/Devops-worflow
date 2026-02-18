# Sprint 1 — Review

## What was delivered

- Core CRUD increment (create, read, update, delete) as implemented in the existing codebase.
- Automated tests (unit/integration style) using Jest + Supertest.
- CI pipeline to run tests on `develop` and `main`.

## Acceptance Evidence

- Passing CI run referencing commit SHA and branch.
- `npm test` console output showing tests passing.
- Sample recorded request/response showing `POST /` returns 302 redirect and `GET /` returns HTML list.

## Demonstration notes

- Start app: `cd app && npm run dev`.
- Use browser or curl to exercise endpoints. During demo, point to CI build link and tests output.
