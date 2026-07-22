# 10 - Performance & Scalability

- Async everywhere; connection pooling sized to expected concurrency (small team — tens, not thousands, of concurrent users).
- Redis for: AI response cache, session/refresh-token handling, hot read-through caches (company settings, workflow config).
- Background jobs (async queue) for anything slow or external: AI calls, document text extraction/scan, report generation, the calendar sweep job, notification fan-out.
- Pagination + filtering on every list endpoint — no unbounded collections returned.
- Deliberate eager-loading on nested payloads (e.g., Project → Documents → Tasks) to avoid N+1 queries.
- Indexes on every foreign key and every field used in search/filter/due-date range queries — the calendar aggregation query in particular depends on due-date indexes across all three source tables.
- Reverse proxy handles static file serving and TLS termination, keeping the app process focused on request handling.
