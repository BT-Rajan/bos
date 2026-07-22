# 09 - Security & Compliance

Built as infrastructure from the first backend pass, not a hardening step at the end.

## Auth & Access
- OAuth2 password flow, JWT access (short-lived) + refresh (rotated on use, stored hashed).
- RBAC enforced via a shared dependency, not per-route conditionals.
- `/public/status` is the one deliberately unauthenticated endpoint — rate-limited hard, since it has no auth to lean on.

## Data Protection
- TLS everywhere (terminated at reverse proxy).
- Secrets via environment/secret manager — never committed.
- Documents encrypted at rest.
- Signed, time-limited download URLs — no exposed storage paths.
- Parameterized queries only (guaranteed by "no raw SQL").

## Audit
- Every write attributable to a user (`created_by`/`updated_by`).
- Generic `audit_log` table + write-interceptor, built once, applies to every module.
- Sensitive actions (government submission, contract finalization, payment status change) specifically reviewed for audit coverage.

## Perimeter
- CORS locked to known frontend origins.
- Rate limiting on `/auth/login` and `/public/status` especially.
- File upload validation: size limits, type allow-list, AV scan.
- Dependency vulnerability scanning in CI.

## AI-Specific
- No AI write access to system-of-record data (see 08-AI-Behaviour.md).
- AI never receives credentials or full user records.

## Backup & Recovery
- Scheduled DB backups.
- Restore tested end-to-end, not assumed to work.
