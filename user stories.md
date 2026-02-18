## User Stories

This file contains prioritized user stories with estimates, acceptance criteria, an assigned sprint, and a short Definition of Done (DoD) for each story to support sprint planning and grading evidence.

### Story 1: Basic Todo Creation

As a user
I want to create new todo tasks
So that I can track my work and responsibilities

Acceptance Criteria:

- User can submit a task via web form or JSON API
- Task is validated (non-empty title)
- Task is saved to MongoDB
- User is redirected to the updated todo list after create
- API: `POST /api/todos` accepts JSON

Priority: High
Story Points: 3
Sprint: Sprint 1
Definition of Done:

- Unit/integration tests for creation exist and pass
- Linting passes and CI green
- DB persistence verified locally and via tests
- Documentation updated (README & examples)

---

### Story 2: Todo List Display

As a user
I want to view all my todos in one place
So that I can see what tasks need to be completed

Acceptance Criteria:

- Homepage displays all todos from database
- Empty state handled gracefully
- API: `GET /api/todos` returns JSON array
- Support filtering by completion status, priority, and category

Priority: High
Story Points: 2
Sprint: Sprint 1
Definition of Done:

- Tests cover list rendering and API response
- Filter query params are documented and tested
- UI empty-state handled and tested

---

### Story 3: Todo Deletion

As a user
I want to delete completed or unwanted todos
So that I can keep my task list clean and relevant

Acceptance Criteria:

- Delete control available for each todo (frontend uses a form POST)
- Frontend delete action posts to `/todo/destroy` with `_key` (no client-side confirmation implemented)
- Todo removed from database permanently
- API: `DELETE /api/todos/:id` removes the todo

Priority: High
Story Points: 2
Sprint: Sprint 1
Definition of Done:

- Tests for deletion both in API and UI
- Confirmation dialog present and tested
- CI green with deletion tests

---

### Story 4: Todo Status Management

As a user
I want to mark todos as complete or incomplete
So that I can track my progress on tasks

Acceptance Criteria:

- API: `PATCH /api/todos/:id` updates completion status (supported)
- Visual distinction for completed vs pending todos (UI displays tasks; no toggle currently)
- Note: web UI currently does not provide a toggle control — updates to `completed` are available via the API or future UI work

Priority: High
Story Points: 3
Sprint: Sprint 1
Definition of Done:

- Tests for toggle behavior and API update
- Visual styling for completed tasks
- CI green with toggle tests

---

### Story 5: Advanced Todo Properties

As a user
I want to set priority, due date, and category for todos
So that I can better organize and prioritize my tasks

Acceptance Criteria:

- Priority levels: low, medium, high (default: medium)
- Optional due date field
- Optional category field for grouping
- API supports these fields on creation (`POST /api/todos`) and they are persisted
- Note: the current `PATCH /api/todos/:id` implementation updates `task` and `completed` only; updating `priority`, `dueDate`, and `category` via PATCH is a planned enhancement

Priority: Medium
Story Points: 5
Sprint: Sprint 2
Definition of Done:

- Schema updated and migration considered
- Tests for create/update with new fields
- UI supports input and filtering for the new fields
- Documentation updated

---

### Story 6: Application Health Monitoring

As a system administrator
I want to monitor application health and performance
So that I can ensure system reliability and troubleshoot issues

Acceptance Criteria:

- Health endpoint `/health` returns system status and uptime
- OpenTelemetry tracing captures request flows
- Winston logging records application events
- Request ID tracking for distributed tracing
- Uptime reporting in health checks

Priority: High
Story Points: 8
Sprint: Sprint 2
Definition of Done:

- `/health` implemented and covered by integration tests
- Tracing configured and validated via test or example traces
- Logs include request-level context and are structured
- CI includes lint and tests for observability code

---

### Story 7: Todo Search and Filtering

As a user
I want to search and filter my todos
So that I can quickly find specific tasks

Acceptance Criteria:

- Filter by completion status, priority, category via query params (implemented in the API)
- Text search across task descriptions (not currently implemented; backlog)
- Filter by date ranges (created, due date) (not currently implemented)
- UI real-time search is a future enhancement

Priority: Medium
Story Points: 5
Sprint: Sprint 2
Definition of Done:

- Search API implemented and tested
- UI filtering controls implemented and tested
- Performance considered for simple datasets

---

### Story 8: Todo Bulk Operations

As a user
I want to perform bulk actions on multiple todos
So that I can efficiently manage large task lists

Acceptance Criteria:

- Select multiple todos via checkboxes
- Bulk delete selected todos
- Bulk mark as complete/incomplete
- Bulk category or priority updates
- Confirmation dialog for bulk operations

Priority: Low
Story Points: 8
Sprint: Backlog (post-Sprint 2)
Definition of Done:

- UI supports multi-select and bulk actions
- API endpoints support bulk updates/deletes
- Tests for bulk flows and confirmation

---

### Story 9: User Authentication & Authorization

As a user
I want secure access to my personal todos
So that my tasks remain private and secure

Acceptance Criteria:

- User registration and login functionality
- JWT token-based authentication
- Password hashing and security
- User-specific todo isolation
- Protected API endpoints require authentication

Priority: Medium
Story Points: 13
Sprint: Backlog (security first before production)
Definition of Done:

- Auth flows implemented with secure storage and hashed passwords
- Tests for auth and protected routes
- Documentation for env vars and token usage
