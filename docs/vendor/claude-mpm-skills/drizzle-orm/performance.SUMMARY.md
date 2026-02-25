# Performance (summary for reviewers)

Upstream reference:
- Performance page (GitHub): https://raw.githubusercontent.com/bobmatnyc/claude-mpm-skills/HEAD/toolchains/typescript/data/drizzle/references/performance.md

## Reviewer takeaways (what to enforce)
### 1) Connection pooling
- Ensure a single pool per process for node deployments.
- Ensure graceful shutdown closes pool connections.
- For serverless, avoid creating a new pool per request; reuse across warm invocations or use HTTP-based drivers.

### 2) Query optimization
- Explicit column projection on wide tables.
- Index-driven filtering and sorting.
- Avoid offset pagination for very large offsets; prefer cursor pagination for stable performance.

### 3) EXPLAIN usage for hotspots
- For slow endpoints, capture an EXPLAIN ANALYZE plan (in non-prod).
- Confirm “Seq Scan” is not happening unintentionally on hot queries.

### 4) Caching strategy
- Cache only when correctness rules are clear (user-specific vs shared).
- Prefer explicit cache keys and TTLs.
- Consider materialized views for expensive aggregated dashboards.

### 5) Batch operations at scale
- Use chunking for batched updates to avoid long-running transactions.
- For very large inserts in Postgres, consider COPY-based ingestion (if operationally appropriate).

### 6) Monitoring and slow query surfacing
- Measure query durations and count per request.
- Flag slow queries and log them without sensitive data.

## Review checklist mapping
- Confirm that list endpoints:
  - have max limits
  - are index-backed
  - avoid pathological pagination modes
- Confirm serverless runtime does not create DB connections per request.
