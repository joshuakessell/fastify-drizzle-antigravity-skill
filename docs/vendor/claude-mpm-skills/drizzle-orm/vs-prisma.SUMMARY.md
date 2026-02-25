# Drizzle vs Prisma (summary for reviewers)

Upstream reference:
- Drizzle vs Prisma page (GitHub): https://raw.githubusercontent.com/bobmatnyc/claude-mpm-skills/HEAD/toolchains/typescript/data/drizzle/references/vs-prisma.md

## Reviewer takeaways (what matters for this skill)
- Drizzle encourages SQL-first patterns with TypeScript inference, which can reduce runtime overhead and avoid a codegen step.
- Prisma can be faster to onboard but adds runtime and translation layers; in some stacks this impacts cold start and bundle size.
- For this skill, the practical relevance is:
  - Reviewers should expect more SQL-shaped code and ensure it is parameterized and validated.
  - The team should document why Drizzle is chosen and how migrations are managed.
  - Security posture must focus on: raw SQL safety, strict validation, and object-level authorization.

## Review checklist mapping
- Ensure you have a documented migration workflow (drizzle-kit or equivalent).
- Ensure raw SQL, if used, is reviewed and tested as carefully as handwritten SQL.
