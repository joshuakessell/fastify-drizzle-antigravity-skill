# Drizzle ORM Query and Schema Patterns (Fastify + Postgres)

This guide captures recurring patterns to enforce when reviewing Drizzle usage for correctness, security, and performance.

## 1) Type safety for JSON columns
- Require `$type<...>()` for JSON fields.
- Avoid `any` and untyped `unknown` for persisted JSON.
- If unknown is unavoidable, gate access behind runtime validation.

## 2) Prefer explicit projections for large tables
- Avoid `select()` without specifying columns on wide or large tables.
- Select only the columns needed for the endpoint’s purpose.

## 3) Use joins and relations intentionally
- Prefer a single query with joins over per-row lookups.
- For list endpoints, watch for N+1 access patterns.
- Use `db.query.<table>.findMany({ with: ... })` when it is clearer and avoids multiple queries.

## 4) Filtering and input validation
- Validate filter fields, operators, and sort keys.
- Apply allowlists for sortable/filterable columns.
- Reject unbounded queries (require pagination and max limits).

## 5) Pagination
- Offset pagination is acceptable for small datasets, but can degrade at scale.
- Prefer cursor pagination for large tables or frequently accessed feeds.
- Always cap `limit` with a server-side maximum.

## 6) Transactions for multi-step writes
Use `db.transaction` whenever:
- Multiple inserts must succeed or fail together
- You create a parent then multiple children
- You must enforce invariant checks across several statements

## 7) Raw SQL safety
- Prefer Drizzle query builders.
- If raw SQL is required, use Drizzle `sql` tagged templates and parameter binding.
- Prohibit string concatenation to build SQL.

## 8) Postgres constraints as correctness primitives
- Use `unique` constraints for natural keys and idempotency protection.
- Use foreign keys and indexes on FK columns for common joins.
- Add CHECK constraints for invariant fields where appropriate.
