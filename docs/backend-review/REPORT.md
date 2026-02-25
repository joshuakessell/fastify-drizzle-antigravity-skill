# Backend Review Report (Template)

## Executive summary
- System reviewed:
- Date:
- Reviewer:
- High-level risk posture:

## Architecture snapshot
- Fastify plugins/hook chain:
- Auth mechanism:
- Validation mechanism:
- Drizzle DB access pattern:
- Background jobs / queues:
- External dependencies:

## Endpoint inventory
| Method | Path | Handler | Auth | Idempotency | Primary tables |
|---|---|---|---|---|---|
|  |  |  |  |  |  |

## Findings
### P0 Critical
- (Finding)

### P1 High
- (Finding)

### P2 Medium
- (Finding)

### P3 Low
- (Finding)

## Remediation plan
1. P0 fixes first (auth bypass, IDOR, duplicate writes under retry, secret leakage)
2. P1 fixes (validation gaps, rate limits, transaction boundaries)
3. P2 fixes (query optimization, redundancy reduction)
4. P3 fixes (cleanup, consistency, docs)

## Quick wins
- Add strict schema validation at route boundaries
- Add unique constraints for natural keys to prevent duplicates
- Add a server-side idempotency key store for retryable POSTs

## Evidence and reproduction notes
- Include request/response examples and relevant code pointers (no secrets).
