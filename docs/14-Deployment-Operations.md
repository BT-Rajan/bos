# 14 - Deployment & Operations

No containers — deployment is a Python virtual environment plus a process supervisor.

## Backend
- `venv` + pinned `requirements.txt`.
- Uvicorn workers under a process supervisor: systemd (Linux) or a Windows Service via NSSM (Windows), matching the team's existing tooling.
- Alembic migrations run as an explicit deploy step, before the service restarts — never manually against production.
- Reverse proxy (Nginx or IIS) in front for TLS termination and static serving.

## Frontend
- Static build artifacts served via the same reverse proxy, or a static host — no separate runtime needed.

## Deploy Script
Pull code → activate venv → install dependencies → run migrations → restart service. Scripted and repeatable, even without containers.

## Observability
- Structured JSON logging throughout.
- Prometheus metrics + Sentry (or equivalent) error tracking from the first deployable pass, not added later.
- `/healthz` and `/readyz` for monitoring/load-balancer checks.

## Backup
- Scheduled DB backups; restore tested end-to-end and documented.
