# Idempotency Design Reference (Fastify + Postgres)

## When to require Idempotency-Key
Use `Idempotency-Key` for POST endpoints that create records and are likely to be retried:
- Payments, orders, subscriptions
- Email/SMS send requests
- Any operation invoked from a UI where the user can double-click or refresh

## Minimal server behavior
1. Client sends:
   - `Idempotency-Key: <uuid>`
   - `Authorization: Bearer <token>`
2. Server computes `requestHash` from:
   - HTTP method + route + authenticated principal + normalized body
3. Server checks idempotency table:
   - If key exists with same hash: return stored response (status + body)
   - If key exists with different hash: reject (409 conflict or 422)
   - If key missing: proceed with transaction, store response, return it

## Postgres table (example)
- idempotency_key (text) primary key
- user_id (uuid/text) not null
- route (text) not null
- request_hash (text) not null
- response_status (int) not null
- response_body (jsonb) not null
- created_at (timestamptz) not null default now()
- expires_at (timestamptz) not null

Add an index on (user_id, created_at) for cleanup jobs.

## Cleanup
- Scheduled job deletes expired keys.
- TTL depends on business process (commonly 24h for creates).

## Constraint-based protection
- Also add unique constraints for natural keys when possible to prevent duplicates under races.
