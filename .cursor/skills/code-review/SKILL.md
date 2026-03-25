---
name: code-review
description: Perform a structured code review for correctness, edge cases, security, performance, and maintainability. Use when reviewing PRs, diffs, or refactors.
---

# Code review

## When to Use

- Reviewing a pull request or patch before merge
- Auditing a change for risk after the fact
- The user asks for a "second pair of eyes"

## Instructions

1. **Understand intent.** Infer what the change is trying to achieve; note if behavior diverges from that intent.
2. **Correctness.** Trace happy path and edge cases (null, empty, max size, concurrency, time zones). Check error handling paths.
3. **Security.** Look for injection (SQL, shell, XSS), authz gaps, secret leakage, unsafe deserialization, path traversal, SSRF patterns.
4. **Performance.** Hot paths, N+1 queries, unbounded loops or allocations, missing indexes for new queries.
5. **Maintainability.** Naming, duplication, test coverage for new logic, migration safety for schema changes.
6. **Be actionable.** Separate must-fix blockers from suggestions; cite specific files/lines when possible.

## Output format

- **Summary** — one short paragraph
- **Blockers** — numbered, each with why and what to change
- **Suggestions** — optional improvements
- **Questions** — only if something is ambiguous
