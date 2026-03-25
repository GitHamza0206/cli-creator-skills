---
name: sql-safe
description: Write and review SQL safely—parameterized queries, migrations, indexes, and least-privilege DB users. Use when touching SQL, ORMs, or schema migrations.
---

# Safe SQL practices

## When to Use

- Writing raw SQL or ORM queries
- Designing migrations or indexes
- Reviewing database access patterns

## Instructions

1. **Parameterized queries.** Never concatenate user input into SQL strings. Use bound parameters / prepared statements.
2. **Least privilege.** App role should not have superuser or broad DDL in production; separate migration role if needed.
3. **Migrations.** Prefer additive, backward-compatible steps when systems run during deploys; document locks and long-running migrations.
4. **Indexes.** Match query predicates and sort orders; avoid redundant indexes; analyze plans for hot queries.
5. **Transactions.** Keep scope small; handle deadlocks with retry where appropriate; choose isolation level deliberately.
6. **PII.** Minimize stored sensitive fields; encrypt at rest per platform; avoid logging query parameters that contain secrets.

## Checklist

- [ ] No dynamic SQL built from unescaped user strings
- [ ] New queries have been explained or EXPLAIN'd for critical paths
