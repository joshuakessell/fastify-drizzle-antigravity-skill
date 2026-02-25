# Backend Review Checklist (Fastify + Drizzle + Postgres)

## A. Inventory
- [ ] Enumerate all routes (method, path, handler)
- [ ] Enumerate hooks (onRequest, preHandler, onSend, onError)
- [ ] Enumerate auth mechanisms (JWT, cookies, API keys, mTLS)
- [ ] Enumerate db tables, constraints, indexes, migrations
- [ ] Enumerate external service calls and timeouts/retries

## B. Idempotency and concurrency safety
- [ ] GET/HEAD have no side effects
- [ ] PUT is idempotent by resource identity
- [ ] DELETE is idempotent (repeat is no-op)
- [ ] POST create endpoints that can be retried support Idempotency-Key or natural unique keys
- [ ] Replayed Idempotency-Key returns same response for same request hash; mismatch rejects
- [ ] Database constraints enforce uniqueness to prevent duplicates under race
- [ ] Multi-step writes are wrapped in transactions
- [ ] Optimistic concurrency is used where overwrites are risky (ETag/If-Match or version field)

## C. Redundancy and request de-duplication
- [ ] No duplicated route logic (shared utilities/services exist)
- [ ] No double-fetch patterns (e.g., insert then select without need; use RETURNING)
- [ ] No N+1 patterns in list endpoints
- [ ] Payloads contain only necessary fields; no over-posting/mass assignment
- [ ] Responses include enough fields to avoid immediate follow-up calls (unless intentionally split)

## D. Validation and error contracts
- [ ] Params/query/body validated at boundary (reject unknown fields)
- [ ] Stable error envelope (code/message/requestId)
- [ ] Correct status codes (401/403/404/409/422/429/5xx)
- [ ] No stack traces or secrets returned to clients

## E. Security controls
- [ ] AuthN and AuthZ enforced (including object-level authorization / IDOR prevention)
- [ ] Rate limits on auth and expensive endpoints
- [ ] CORS configured minimally; credentials only when required
- [ ] CSRF protection if cookie-auth
- [ ] Output filtering prevents sensitive field exposure
- [ ] Secrets hygiene: no secrets in logs; redaction in structured logger
- [ ] Safe file upload handling (if present): size/type limits, storage controls
- [ ] SSRF protections on outbound fetches (allowlist + URL parsing)

## F. Observability and operability
- [ ] Request ID propagation (X-Request-Id) and correlation in logs
- [ ] Security-relevant audit logs (auth changes, role changes, sensitive actions)
- [ ] Metrics: latency, error rate, db query count/time, idempotency hits

## G. Drizzle-specific red flags
See `docs/backend-review/RED_FLAGS.md`.

- [ ] No untyped JSON columns (`$type<...>()` enforced)
- [ ] No raw SQL string concatenation (only `sql` tagged templates with bindings)
- [ ] Transactions cover multi-step writes
- [ ] No unbounded selects in production (pagination required)
- [ ] Indexes exist for foreign keys and common filters
- [ ] Large-table queries use explicit projections


## H. Embedded reference summaries to consult
- [ ] Advanced schemas patterns reviewed (enums, json/jsonb typing, composite keys, constraints, tenant isolation)
- [ ] Query patterns reviewed (CTEs, safe raw SQL, dynamic filters allowlists, prepared statements, locking)
- [ ] Performance guidance reviewed (pooling, cursor pagination, EXPLAIN for hotspots, caching rules)
