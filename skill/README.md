# fastify-drizzle-backend-reviewer (Google Antigravity Skill)

This repository contains **files and guardrails** that support a repeatable, audit-friendly backend review process for:
- Fastify + TypeScript
- Drizzle ORM
- PostgreSQL
- React/TypeScript frontend consumers

The review focuses on:
- Idempotency and retry safety
- Enterprise coding standards
- Redundancy elimination and request/DB optimization
- Request-purpose alignment (only needed data; enough data returned to avoid follow-up calls)
- Security posture (authn/authz, validation, injection, CORS/CSRF, rate limiting, secrets hygiene)

## Quick start
1. Copy these files into your repo (or keep as a template repo).
2. Ensure your backend has a committed lockfile (package-lock.json / pnpm-lock.yaml / yarn.lock).
3. Enable GitHub Actions workflows in `.github/workflows/`.
4. Run the local checks:
   - `npm run security:lint`
   - `npm run security:deps`
   - `npm run security:sbom`

## Supply chain and skill scanning
- Gen Agent Trust Hub provides a skill scanner intended to detect hidden malicious behavior, unsafe data handling, and other risks. citeturn2search3
- Socket provides GitHub Actions/CLI integration to scan dependencies and supply-chain risks. citeturn3view1
- Snyk provides GitHub Actions integration and SARIF upload patterns for code scanning workflows. citeturn2search2turn2search7


## Navigation (loadable references)
- `docs/backend-review/DRIZZLE_QUERY_PATTERNS.md`: Drizzle patterns for joins, pagination, transactions, raw SQL safety. citeturn0view0
- `docs/backend-review/RED_FLAGS.md`: quick stop-check list for common Drizzle pitfalls. citeturn0view0
- `docs/backend-review/PERFORMANCE_GUIDE.md`: optimization checklist for queries and pooling.


## Embedded upstream reference summaries (offline)
These are summaries derived from the drizzle-orm skill’s referenced subpages. citeturn0view0turn3view0turn3view1turn3view2

- `docs/vendor/claude-mpm-skills/drizzle-orm/advanced-schemas.SUMMARY.md`
- `docs/vendor/claude-mpm-skills/drizzle-orm/query-patterns.SUMMARY.md`
- `docs/vendor/claude-mpm-skills/drizzle-orm/performance.SUMMARY.md`
- `docs/vendor/claude-mpm-skills/drizzle-orm/vs-prisma.SUMMARY.md`
