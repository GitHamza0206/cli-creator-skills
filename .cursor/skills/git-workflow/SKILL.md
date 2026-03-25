---
name: git-workflow
description: Apply solid Git hygiene—branching, commits, rebases vs merges, and PR descriptions. Use when the user asks about git operations or preparing changes for review.
---

# Git workflow

## When to Use

- Preparing commits or a pull request
- Deciding branch strategy for a fix or feature
- Cleaning up history before merge (when team policy allows)

## Instructions

1. **Branch from the agreed base** (usually `main` or `develop`). Use descriptive branch names (`fix/login-redirect`, `feat/export-csv`).
2. **Commits.** Small, logical commits; imperative subject line (~50 chars); body explains *why* when the diff is not obvious. Do not commit secrets or large generated artifacts unless required.
3. **PR scope.** One coherent change per PR when possible; link issues; describe user-visible behavior and risk.
4. **Rebase vs merge.** Follow team convention. Rebase for a linear history when allowed; avoid rewriting public shared branches without coordination.
5. **Conflict resolution.** Understand both sides; preserve intended behavior; run tests after resolving.
6. **Revert policy.** Prefer `git revert` for shared history over destructive resets on shared branches.

## Checklist

- [ ] `.gitignore` covers local env and build output
- [ ] CI passes or failures are explained in the PR
