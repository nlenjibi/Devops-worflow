# 1️⃣ Project Overview

## Project Title

**DevOps Todo REST API**

## Product Vision

A scalable, cloud-native Todo management system that demonstrates modern DevOps practices through containerization, automated testing, and observability. The API provides both web interface and REST endpoints for task management with enterprise-grade monitoring and deployment capabilities.

## Description of the Todo REST API

The Todo REST API is a full-stack Node.js application built with Express.js and MongoDB that provides comprehensive task management functionality. It features:

- **Dual Interface**: Web UI (EJS templates) and REST API endpoints
- **Core CRUD Operations**: Create, read, update, and delete todos
- **Advanced Features**: Task prioritization, categorization, due dates, and completion tracking
- **Enterprise Observability**: OpenTelemetry tracing, Winston logging, and health monitoring
- **DevOps Ready**: Dockerized with CI/CD pipeline and automated testing

## Deployment Target

**Vercel** (serverless Node.js deployment) with MongoDB Atlas for database persistence

---

# 2️⃣ Product Backlog

## MVP Explanation

The Minimum Viable Product focuses on core task management functionality with robust DevOps practices. Users can create, view, update, and delete todos through both web interface and API, with full observability and automated deployment pipeline.

## Backlog Prioritization Logic

1. **High Priority**: Core CRUD functionality and deployment infrastructure
2. **Medium Priority**: Enhanced features and user experience improvements
3. **Low Priority**: Advanced integrations and optimization features

## Definition of Done (DoD)

- [ ] Code committed to version control
- [ ] Unit and integration tests written and passing
- [ ] Code passes linting standards
- [ ] CI pipeline passing (lint + test)
- [ ] Deployed to Vercel successfully
- [ ] MongoDB connection secured via environment variables
- [ ] Health endpoint responding correctly

## Tests & Coverage (current)

- Integration and request tests using Jest + Supertest are located under `app/test/` and include:
  - `api.test.js` (API create/list/filter flows)
  - `todos.test.js` (integration: model + DB)
  - `front.test.js` (frontend route rendering with mocked model)
  - `health.test.js` (health endpoint)
  - `tracing.test.js` (request id / tracing middleware)

Note: some integration tests require a running MongoDB instance; front-route tests mock the model to avoid DB dependency.

---

## User Stories

### Story 1: Basic Todo Creation

**As a** user  
**I want** to create new todo tasks  
**So that** I can track my work and responsibilities

**Acceptance Criteria:**

- User can submit a task via web form
- Task is validated (non-empty)
- Task is saved to MongoDB
- User is redirected to updated todo list
- API endpoint `POST /api/todos` accepts JSON requests

**Priority:** High  
**Story Points:** 3  
**Reasoning:** Core functionality, straightforward implementation with validation

---

### Story 2: Todo List Display

**As a** user  
**I want** to view all my todos in one place  
**So that** I can see what tasks need to be completed

**Acceptance Criteria:**

- Homepage displays all todos from database
- Empty state handled gracefully
- API endpoint `GET /api/todos` returns JSON array
- Support filtering by completion status, priority, and category

**Priority:** High  
**Story Points:** 2  
**Reasoning:** Essential read functionality, minimal complexity

---

### Story 3: Todo Deletion

**As a** user  
**I want** to delete completed or unwanted todos  
**So that** I can keep my task list clean and relevant

**Acceptance Criteria:**

- Delete button available for each todo
- Frontend delete action posts to `/todo/destroy` with `_key` (no client-side confirmation implemented)
- Todo removed from database permanently
- API endpoint `DELETE /api/todos/:id` removes specific todo

**Priority:** High  
**Story Points:** 2  
**Reasoning:** Basic CRUD operation, simple implementation

---

### Story 4: Todo Status Management

**As a** user  
**I want** to mark todos as complete or incomplete  
**So that** I can track my progress on tasks

**Acceptance Criteria:**

- API endpoint `PATCH /api/todos/:id` updates completion status (supported)
- Visual distinction for completed vs pending todos (UI displays tasks; no toggle control currently)
- Note: web UI currently does not provide a toggle control — updates to `completed` are available via the API or future UI work

**Priority:** High  
**Story Points:** 3  
**Reasoning:** Core functionality requiring UI and API updates

---

### Story 5: Advanced Todo Properties

**As a** user  
**I want** to set priority, due date, and category for todos  
**So that** I can better organize and prioritize my tasks

**Acceptance Criteria:**

- Priority levels: low, medium, high (default: medium)
- Optional due date field
- Optional category field for grouping
- API supports these fields on creation (`POST /api/todos`) and they are persisted
- Note: the current `PATCH /api/todos/:id` implementation updates `task` and `completed` only; updating `priority`, `dueDate`, and `category` via PATCH is a planned enhancement

**Priority:** Medium  
**Story Points:** 5  
**Reasoning:** Enhanced functionality requiring schema updates and UI changes

---

### Story 6: Application Health Monitoring

**As a** system administrator  
**I want** to monitor application health and performance  
**So that** I can ensure system reliability and troubleshoot issues

**Acceptance Criteria:**

- Health endpoint `/health` returns system status
- OpenTelemetry tracing captures request flows
- Winston logging records application events
- Request ID tracking for distributed tracing
- Uptime reporting in health checks

**Priority:** High  
**Story Points:** 8  
**Reasoning:** Complex observability setup, critical for production deployment

---

### Story 7: Automated Testing & CI Pipeline

**As a** developer  
**I want** automated testing and continuous integration  
**So that** I can deploy with confidence and maintain code quality

**Acceptance Criteria:**

- Jest unit tests for all API endpoints
- Supertest integration tests for request/response flows
- ESLint code quality checks
- GitHub Actions CI pipeline runs on push/PR
- All tests must pass before deployment

**Priority:** High  
**Story Points:** 5  
**Reasoning:** Essential DevOps practice, moderate complexity for setup

---

### Story 8: Containerized Deployment

**As a** DevOps engineer  
**I want** the application containerized with Docker  
**So that** I can deploy consistently across environments

**Acceptance Criteria:**

- Dockerfile builds application image successfully
- Docker Compose orchestrates app and database services
- Environment variables configure database connections
- Container runs application on specified port
- Multi-stage build optimizes image size

**Priority:** High  
**Story Points:** 4  
**Reasoning:** Critical for cloud deployment, well-defined requirements

---

### Story 9: Todo Search and Filtering

**As a** user  
**I want** to search and filter my todos  
**So that** I can quickly find specific tasks

**Acceptance Criteria:**

- Text search across task descriptions
- Filter by completion status, priority, category
- Filter by date ranges (created, due date)
- Search results update in real-time
- API supports query parameters for filtering

**Priority:** Medium  
**Story Points:** 5  
**Reasoning:** User experience enhancement, requires search implementation

---

### Story 10: Todo Bulk Operations

**As a** user  
**I want** to perform bulk actions on multiple todos  
**So that** I can efficiently manage large task lists

**Acceptance Criteria:**

- Select multiple todos via checkboxes
- Bulk delete selected todos
- Bulk mark as complete/incomplete
- Bulk category or priority updates
- Confirmation dialog for bulk operations

**Priority:** Low  
**Story Points:** 8  
**Reasoning:** Advanced feature, complex UI and API changes required

---

### Story 11: User Authentication & Authorization

**As a** user  
**I want** secure access to my personal todos  
**So that** my tasks remain private and secure

**Acceptance Criteria:**

- User registration and login functionality
- JWT token-based authentication
- Password hashing and security
- User-specific todo isolation
- Protected API endpoints require authentication

**Priority:** Medium  
**Story Points:** 13  
**Reasoning:** Significant feature requiring security implementation and data model changes

---

### Story 12: Performance Optimization & Caching

**As a** system administrator  
**I want** optimized application performance  
**So that** users experience fast response times

**Acceptance Criteria:**

- Database query optimization with indexes
- Redis caching for frequently accessed data
- API response compression
- Static asset optimization
- Performance monitoring and alerting

**Priority:** Low  
**Story Points:** 8  
**Reasoning:** Optimization feature, requires performance analysis and caching setup
