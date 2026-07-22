# 13 - Testing Strategy

## Backend
- pytest + pytest-asyncio + httpx.AsyncClient.
- One test module per backend module, same folder layout as the code.
- Contract tests: response shapes checked against `05-API-Reference.md`/`04-Data-Model.md`, so frontend and backend never silently drift.
- Full coverage on services and repositories (business logic and query correctness matter most).
- A dedicated **cross-module integration test** for the calendar/escalation engine once tasks, submissions, and milestones all feed it — timezone edge cases at day boundaries, manager rollup correctness across all three source types.

## Frontend
- Component tests for design-system components (once, reused confidence for every consumer).
- View-level tests for Calendar (due-chip rendering, status coloring, deep-link navigation) and Workspace list/detail flows.

## Environments
- Separate test database, migrations applied fresh in CI before the suite runs.
