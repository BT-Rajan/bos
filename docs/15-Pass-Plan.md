# 15 - Pass Plan (Frontend + Backend, Unified)

Same discipline as `12-Coding-Standards.md`: one pass, one commit, one push. Backend passes 1-73 are as stress-tested in the ServiceOS planning work; frontend passes are new here, interleaved where a working end-to-end slice makes sense sooner.

## Backend (Passes 1-73)

**Phase 0 — Foundation (1-9):** scaffold, config (incl. business timezone), logging, DB/Alembic, venv setup, CI, health checks, audit log infra.
**Phase 1 — Auth, Users, Baseline Security (10-16):** JWT auth, RBAC, rate limiting/CORS, user CRUD.
**Phase 2 — Company & Clients (17-20).**
**Phase 3 — Projects Core (21-26):** projects, workspace tab scaffolding, timeline.
**Phase 4 — Tasks, Generic Escalation, Calendar (27-35):** the shared engine, notifications (built complete once), calendar (tasks only), manager rollup.
**Phase 5 — Documents (36-41):** storage, versioning, scan, encryption at rest.
**Phase 6 — Government Center (42-47):** forms, authorities, submissions, calendar/escalation reuse.
**Phase 7 — Contracts, Quotations, Payments (48-54):** milestones, calendar/escalation reuse.
**Phase 8 — Cross-Module Calendar Integration Test (55).**
**Phase 9 — Workflows, Messages, Search (56-59).**
**Phase 10 — AI Module (60-65).**
**Phase 11 — Reports, Admin, Customer Portal (66-69).**
**Phase 12 — Hardening, Backup, Launch (70-73).**

## Frontend (Passes F1-F24)

**Phase F0 — Design System Foundation (F1-F4)**
F1. Design tokens (color/type/spacing), Button/Input/Select primitives.
F2. Table, Card, Status Badge components.
F3. Modal/Drawer, Empty State, Skeleton Loader.
F4. Design-system Storybook/preview page + component tests.

**Phase F1 — Shell & Auth (F5-F7)**
F5. App shell, routing, auth views (login/reset).
F6. Home shell: Calendar/Workspace top-level split, nav.
F7. Global chrome: Search bar, Notifications bell, Messages, AI Assistant drawer shell.

**Phase F2 — Calendar (F8-F10)**
F8. Calendar view: month/week/day toggle, due-chip rendering, status coloring.
F9. Calendar deep-links into Workspace (task/submission/milestone → detail).
F10. Manager/admin rollup toggle on Calendar.

**Phase F3 — Workspace Core (F11-F15)**
F11. Clients: list/search/detail/create/edit.
F12. Projects: list/search/detail shell with tab navigation.
F13. Project tabs: Overview, Tasks (due-date picker mandatory, status/follow-up/escalate actions).
F14. Project tabs: Documents (upload, versions, viewer).
F15. Project tabs: Timeline (activity feed, read-only render).

**Phase F4 — Government, Contracts, Financials (F16-F19)**
F16. Government Center: forms library, authorities, submissions.
F17. Contracts: list/detail, milestones view (feeds Calendar).
F18. Quotations: list/detail.
F19. Payments: list/detail, status.

**Phase F5 — Cross-Cutting UI (F20-F22)**
F20. Workflows admin UI.
F21. Search results view.
F22. Notifications feed + preferences UI.

**Phase F6 — AI, Reports, Admin (F23-F24)**
F23. AI Assistant drawer: full interaction (summary/details/confidence/suggested actions), AI history view (admin), AI config UI.
F24. Reports dashboard, remaining Admin screens (Users & Roles, Company Settings), Customer Portal status page.

## Sequencing Note

Frontend Phase F2 (Calendar) can start once Backend Pass 32 (tasks-only calendar endpoint) is live — it doesn't need to wait for Phases 6-7's calendar extensions, since the aggregation shape doesn't change, only the sources feeding it. This is the direct payoff of the shared-engine design in `07-Calendar-Escalation-Engine.md`: frontend and backend can both build against a stable contract early.
