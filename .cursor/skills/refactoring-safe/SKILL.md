---
name: refactoring-safe
description: Refactor code safely—small steps, tests, and behavior preservation. Use when restructuring without intended feature changes.
---

# Safe refactoring

## When to Use

- Renaming, extracting functions, or reorganizing modules
- Paying down technical debt without changing external behavior
- Preparing code for a larger feature

## Instructions

1. **Preserve behavior first.** Clarify what "same behavior" means (public API, UI, persisted data).
2. **Mechanical before clever.** Prefer compiler-assisted renames, extract method, move file—one category of change per commit when possible.
3. **Test safety net.** Run existing tests after each step; add characterization tests if coverage is thin before risky edits.
4. **API compatibility.** Deprecate rather than break when consumers are unknown; document migration windows.
5. **Data migrations.** Separate schema from code deploy when zero-downtime is required; verify rollback path.
6. **Review diff size.** Large refactors: split PRs or use clear commits so reviewers can follow intent.

## Anti-patterns

- Mixing refactors with feature changes in the same commit without clear separation
- Deleting "unused" code without verifying dynamic use (reflection, DI, config)
