# 16 - Effort Estimate (Lines of Code)

Order-of-magnitude, implementation LOC only (excludes migrations, generated boilerplate, third-party code). Assumes the tightly-connected architecture in `06-Architecture.md`.

## Backend

| Area | Est. LOC |
|---|---:|
| Core infra (config, logging, DB, auth deps, audit log, rate limiting, background jobs) | 800–1,200 |
| Auth & Users | 500–700 |
| Company & Clients | 400–600 |
| Projects + Timeline | 700–1,000 |
| Tasks + Calendar + Escalation engine (shared) | 1,200–1,800 |
| Documents | 700–1,000 |
| Government Center | 500–700 |
| Contracts, Quotations, Payments | 900–1,300 |
| Workflows, Messages, Notifications, Search | 900–1,300 |
| AI module | 900–1,300 |
| Reports, Admin, Customer Portal | 700–1,000 |
| Tests | 2,500–3,500 |
| **Backend total** | **~10,700–15,600** |

## Frontend

| Area | Est. LOC |
|---|---:|
| Design system | 1,200–1,800 |
| Auth | 300–400 |
| Home shell (Calendar/Workspace) | 400–600 |
| Calendar view | 900–1,300 |
| Task management UI | 800–1,200 |
| Project Workspace (search/list/detail/tabs) | 1,500–2,200 |
| Documents UI | 600–900 |
| Government Center UI | 700–1,000 |
| Contracts/Quotations/Payments UI | 900–1,300 |
| Admin UI | 800–1,200 |
| AI Assistant panel | 500–700 |
| Shared services/store | 700–1,000 |
| **Frontend total** | **~9,900–14,600** |

## Grand Total

**~20,000–30,000 LOC.**

The range's biggest swing factor is test depth and how far "crisp" UI polish extends in practice — treat this as planning-level, not committed, and expect the real number to firm up once early passes establish actual per-module velocity.
