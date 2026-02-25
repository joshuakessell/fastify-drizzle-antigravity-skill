# Red Flags (Stop and Reconsider)

Borrowed and adapted from the referenced Drizzle skill’s “Red Flags” section. citeturn0view0

- Using `any` or untyped `unknown` for JSON columns without `$type<...>()`
- Building raw SQL strings without Drizzle’s `sql` tagged template and parameter binding
- Not using transactions for multi-step data modifications
- Fetching all rows without pagination in production queries
- Missing indexes on foreign keys or frequently queried columns
- Using `select()` without specifying columns for large tables
