---
name: documentation
description: Write or improve technical documentation—READMEs, API docs, runbooks, and inline comments where they add value. Use when the user asks for docs or onboarding clarity.
---

# Documentation

## When to Use

- New project or feature needs a README or overview
- Public or internal API needs usage examples
- Operators need runbooks for deploy, rollback, or incidents

## Instructions

1. **Start with the reader.** Identify audience (new dev, API consumer, on-call). Put prerequisites and quickstart first.
2. **README baseline.** What it does, how to install/run, how to test, how to configure env vars, where architecture is explained.
3. **API docs.** Authentication, base URL, error format, pagination, rate limits, and copy-pasteable examples (curl or SDK).
4. **Runbooks.** Symptom → checks → mitigation → escalation; include dashboards/log queries if applicable.
5. **Inline comments.** Explain *why* and non-obvious invariants; avoid narrating what the code already says.
6. **Keep docs close to code.** Update docs in the same change when behavior changes.

## Checklist

- [ ] Commands in docs were verified or clearly marked as illustrative
- [ ] Breaking changes are called out with migration steps
