# Query Patterns (summary for reviewers)

Upstream reference:
- Query Patterns page (GitHub): https://raw.githubusercontent.com/bobmatnyc/claude-mpm-skills/HEAD/toolchains/typescript/data/drizzle/references/query-patterns.md

## Reviewer takeaways (what to enforce)
### 1) Subqueries and EXISTS
- Use EXISTS/NOT EXISTS for “has related rows” checks, but keep them parameterized.
- Prefer join + group when it is clearer and performant, but verify cardinality and duplicates.

### 2) CTEs (including recursive)
- CTEs can improve readability for complex workflows (top-N, hierarchical data).
- Treat recursive CTEs as potentially expensive; enforce bounds and indexes.

### 3) Raw SQL usage
- Allow raw SQL only via Drizzle `sql` tagged templates with parameter binding.
- Prohibit string concatenation for SQL.
- Ensure raw queries have clear test coverage, since they bypass some builder safety.

### 4) Dynamic filters
- Build filters using typed condition composition.
- Validate incoming filter operators and fields using allowlists.
- Reject “free-form” SQL fragments from clients.

### 5) Aggregations, window functions
- Verify endpoints using window functions have bounded result sets.
- Ensure groupBy + having queries have supporting indexes.

### 6) Prepared statements and hot paths
- Consider prepared statements for high-traffic endpoints where supported.
- Ensure placeholders are not confused with string templating.

### 7) Batch operations
- Prefer upsert patterns (`onConflictDoNothing`, `onConflictDoUpdate`) with the correct unique target.
- Use transactions around batch updates when partial success is not acceptable.

### 8) Locking strategies
- Use row-level locks only when necessary.
- When using `SKIP LOCKED`, ensure the work queue semantics are correct and observable.

## Review checklist mapping
- Identify complex endpoints and confirm they use:
  - allowlisted filters and sort keys
  - query timeouts for expensive queries
  - pagination and max limits
  - safe raw SQL
