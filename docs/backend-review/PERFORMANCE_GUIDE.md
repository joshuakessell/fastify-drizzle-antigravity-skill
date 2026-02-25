# Performance Guide (Fastify + Drizzle + Postgres)

## Query efficiency checks
- Prefer `returning()` to avoid insert then select round-trips.
- Avoid N+1 patterns; fetch related records with joins or Drizzle relations.
- Apply `limit` and server-side max limits on every list endpoint.
- Validate sort keys and apply indexes that match common filters and order-by.

## Connection and pooling
- Ensure a single pool is initialized per process (avoid per-request pools).
- Confirm pool size and timeouts match deployment environment.

## Prepared statements
- Prefer parameterized queries (Drizzle default) rather than interpolated strings.
- For hot paths, consider prepared statements if driver and runtime allow.

## Edge and serverless considerations
- If running in serverless, confirm pool strategy is compatible (or use a serverless-friendly driver).
- Avoid long transactions under high concurrency.
