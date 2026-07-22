# 06 - Architecture

## Repo Structure (frontend + backend, one repo)

```
bos/
├── docs/               # this documentation set
├── backend/
│   └── app/
│       ├── core/       # config, security, logging, audit, background jobs
│       ├── db/
│       ├── calendar/    # the shared Calendar/Escalation engine — see 07
│       └── modules/     # auth, users, company, clients, projects, tasks,
│                        # documents, government, contracts, quotations,
│                        # payments, workflows, timeline, messages,
│                        # notifications, search, ai, reports
├── frontend/
│   └── src/
│       ├── design-system/
│       ├── views/       # Home (Calendar/Workspace), Projects, Clients, ...
│       ├── components/
│       ├── services/    # API client, one file per backend module
│       └── store/
└── tests/
```

## Why Tightly Connected (and what it costs)

Tasks, government submissions, and contract milestones all funnel through **one shared Calendar/Escalation engine** (`backend/app/calendar/`) rather than three independent modules each implementing their own due-date and escalation logic behind a generic interface.

**What this buys:**
- One state machine to get right, not three — fewer bugs, less code (see `16-Effort-Estimate.md`).
- A change to escalation behavior (e.g., adding a new status, changing notification timing) happens once and applies everywhere automatically.
- Calendar aggregation is a single `UNION` query against a shared shape, not three separate aggregation paths to keep in sync.

**What this costs, honestly:**
- Tasks, government submissions, and contract milestones can no longer evolve independently at the data layer — a schema change to the shared due-date/status shape touches all three domains at once.
- This is the wrong choice for a multi-tenant platform serving several unrelated clients, or a team larger than ~20 where module ownership needs hard boundaries. For one client, one product, one small team, it's the right one.

## Layering (within backend/app)

```
Router → Service → Repository → Models
```
Same rules as before: routers never touch the ORM directly; services hold business logic and permission checks; repositories are the only layer that queries; the calendar/escalation engine is called by task/submission/milestone services, not duplicated inside them.

## Frontend Principles

- One design-system package, consumed by every view — no per-module ad-hoc styling.
- Services layer mirrors backend modules 1:1, matching `05-API-Reference.md` exactly, so a change on one side has an obvious counterpart on the other.
- Calendar and Workspace are sibling top-level views under Home, not nested inside each other.
