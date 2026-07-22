# 05 - API Reference

Base path: `/api`. All endpoints except `/auth/*` and `/public/*` require a valid access token. All list endpoints support `?page=&page_size=&search=&filter[...]=`.

## Auth
- `POST /auth/login`
- `POST /auth/refresh`
- `POST /auth/logout`
- `POST /auth/password-reset`

## Calendar (the shared engine's public surface)
- `GET /calendar?from=&to=&user=` — aggregated due items (tasks + submissions + milestones) for a user
- `GET /calendar/team` — manager/admin rollup, team-wide
- `POST /escalations/{entity_type}/{entity_id}/follow-up`
- `POST /escalations/{entity_type}/{entity_id}/reschedule`
- `POST /escalations/{entity_type}/{entity_id}/escalate`
- `POST /escalations/{entity_type}/{entity_id}/complete`

## Users / Roles
- `GET/POST /users`, `GET/PUT /users/{id}`
- `GET/POST /roles`

## Company
- `GET/PUT /company`

## Clients
- `GET/POST /clients`, `GET/PUT/DELETE /clients/{id}`

## Projects
- `GET/POST /projects`, `GET/PUT/DELETE /projects/{id}`
- `GET /projects/{id}/timeline`

## Tasks
- `GET/POST /tasks`, `GET/PUT/DELETE /tasks/{id}`
- `GET /tasks/mine`
- `GET /projects/{id}/tasks`

## Documents
- `GET/POST /documents`, `GET /documents/{id}`, `DELETE /documents/{id}`
- `GET /documents/{id}/versions`
- `GET /documents/{id}/download` (signed URL)

## Government Center
- `GET/POST /government/forms`
- `GET/POST /government/authorities`
- `GET/POST /government/submissions`, `GET/PUT /government/submissions/{id}`

## Contracts / Quotations / Payments
- `GET/POST /contracts`, `GET/PUT /contracts/{id}`
- `GET/POST /contracts/{id}/milestones`
- `GET/POST /quotations`, `GET/PUT /quotations/{id}`
- `GET/POST /payments`
- `POST /payments/webhook`

## Workflows
- `GET/POST /workflows`

## Messages / Notifications
- `GET/POST /messages`
- `GET /notifications`, `PUT /notifications/{id}/read`
- `GET/PUT /notifications/preferences`

## Search
- `GET /search?q=` — across clients/projects/documents/tasks/government submissions

## AI
- `POST /ai/complete`
- `GET/PUT /ai/config`
- `GET /ai/history`

## Reports
- `GET /reports/overview`
- `GET /reports/overdue-trends`
- `GET /reports/financial-summary`
- `GET /reports/compliance`

## Public (unauthenticated, rate-limited)
- `POST /public/status` — mobile number + project ID → status/timeline only

## Ops
- `GET /healthz`, `GET /readyz`
