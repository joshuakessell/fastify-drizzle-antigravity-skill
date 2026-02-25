# Data Handling and Redaction

## Sensitive data categories
- Access tokens (JWTs, API keys)
- Session cookies
- Database URLs, credentials
- Passwords and password reset tokens
- Encryption keys
- PII fields (email, phone, address, SSN, etc.)

## Rules
- Never log raw `Authorization` headers.
- Redact known secret-like patterns in logs (token prefixes, base64 blobs).
- Do not include stack traces or internal error objects in API responses.
- Use structured logging and explicit allowlists of safe fields.

## Suggested log fields
- requestId, route, method, statusCode, durationMs
- userId (if authenticated), tenantId (if multi-tenant)
- errorCode (stable), errorCategory

## Incident response
- If secret leakage is suspected, rotate keys immediately and invalidate sessions.
