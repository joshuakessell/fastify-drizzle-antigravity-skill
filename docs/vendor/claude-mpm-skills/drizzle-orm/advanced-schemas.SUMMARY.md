# Advanced Schemas (summary for reviewers)

Upstream reference:
- Advanced Schemas page (GitHub): https://raw.githubusercontent.com/bobmatnyc/claude-mpm-skills/HEAD/toolchains/typescript/data/drizzle/references/advanced-schemas.md

## Reviewer takeaways (what to enforce)
### 1) Custom types and enums
- Prefer database-native enums (Postgres) or constrained text where enums are not available.
- Ensure enum values are validated at the API boundary, not only at DB level.

### 2) Typed JSON fields
- Require typed JSON (`$type<...>()`) for JSON/JSONB columns.
- Pair typed JSON with runtime validation for untrusted input (e.g., Zod validation before persistence).
- Avoid storing arbitrary JSON blobs unless the domain truly requires it.

### 3) Arrays and array querying
- Ensure array columns have clear semantics and are indexed where appropriate (GIN indexes for Postgres arrays often apply).
- Validate any filters that use array operators (allowlist the permitted operations).

### 4) Indexing patterns
- Confirm indexes match real query patterns (filter + sort combos).
- Partial indexes: use them for “active row” constraints (e.g., unique on email where deletedAt IS NULL).
- Full text search: treat `to_tsvector` indexes as first-class schema assets; document how search is performed.

### 5) Composite keys
- Composite primary keys are appropriate for join tables and key-value preference tables.
- Ensure all referencing queries pass both key parts and do not fall back to “first match” behavior.

### 6) Check constraints and generated columns
- Use check constraints for invariants like non-negative prices and discount < price.
- Generated columns can normalize derived fields and reduce duplication but must be consistent with writes.

### 7) Multi-tenant patterns
- If multi-tenant, explicitly define tenant isolation:
  - App-enforced tenant scoping on every query, or
  - Postgres RLS, plus setting tenant context per request, plus tests proving isolation.
- Avoid “schema per tenant” unless operationally justified and automated.

## Review checklist mapping
- Schema files: verify enums, json/jsonb typing, constraints, indexes, and FK references.
- Migrations: verify constraints and partial indexes exist in migrations (not only in TypeScript schema).
- Routes/services: verify tenant scoping is not optional or easy to bypass.
