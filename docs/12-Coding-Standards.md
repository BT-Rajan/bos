# 12 - Coding Standards

## Backend
- Async-first throughout; no blocking calls in the request path.
- No raw SQL — ORM/Core expression language only.
- Small, single-responsibility functions (~40-line guideline).
- Routers never touch the ORM; services never import ORM models directly (call repositories); repositories are the only layer that queries.
- The calendar/escalation engine is called, never re-implemented, by task/submission/milestone services.
- No TODOs or commented-out code left in committed work.

## Frontend
- Design-system components used everywhere a matching pattern exists — no one-off styled equivalents.
- Services layer mirrors the backend API 1:1 (`05-API-Reference.md`).
- Shared state (auth, notifications, current user) lives in one store module, not duplicated per view.

## Process (both sides)
```
Implement → Test → Build/run clean → Commit → Push → Stop
```
One pass, one commit, one push — never move to the next pass with the current one uncommitted.
