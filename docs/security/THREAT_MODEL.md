# Threat Model (Fastify + Drizzle + Postgres)

## Assets
- User identities and sessions/tokens
- PII (if present)
- Authorization rules (roles, ownership)
- Financial/order records (if present)
- Database credentials and encryption keys
- Audit logs

## Trust boundaries
1. Browser client (React)
2. API gateway / Fastify server
3. Database (Postgres)
4. Third-party services (email, payments, storage)

## Primary threat categories
- Auth bypass and privilege escalation
- IDOR/BOLA (object-level auth failures)
- Injection (SQL via raw queries; command injection; template injection)
- CSRF (if cookie sessions)
- CORS misconfiguration + credential leakage
- Replay and duplicate-write bugs (missing idempotency)
- Supply-chain compromise (malicious npm packages, compromised actions)
- Secrets leakage (logs, error traces, client responses)
- DoS and abuse (missing rate limits, unbounded queries)

## Controls checklist
- Strong authn + explicit authz per route (including ownership checks)
- Validation at boundaries (reject unknown fields)
- Idempotency keys and unique constraints for retryable creates
- Central error handling with stable error codes (no stack traces to clients)
- Rate limiting and request size limits
- Secure headers and minimal CORS policy
- Structured logs with redaction (never log tokens)
- Dependency scanning in CI and lockfile enforcement
