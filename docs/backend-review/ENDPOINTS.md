# Endpoint Specifications (Template)

## Conventions
- Success envelope: `{ "data": ..., "meta": ... }`
- Error envelope: `{ "error": { "code": "...", "message": "...", "requestId": "..." } }`
- Authentication: `Authorization: Bearer <token>` (or cookie session; specify explicitly)
- Idempotency: `Idempotency-Key: <uuid>` for retryable creates

---

## (METHOD) /path
**Purpose**
- What user workflow this supports.

**Auth**
- Required: (yes/no)
- Policy: (role/resource ownership)
- Token type: (JWT/cookie/api key)

**Request**
- Headers:
- Params:
- Query:
- Body schema:

**Response**
- 200/201:
- Error codes:

**Idempotency**
- Classification:
- Enforcement approach:
- Replay behavior:

**DB interactions**
- Tables:
- Constraints:
- Transaction boundary:
- Index requirements:

**Observability**
- Logs:
- Metrics:
