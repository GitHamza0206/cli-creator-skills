---
name: debugging-systematic
description: Debug failures systematically—reproduce, narrow scope, form hypotheses, verify with evidence. Use when tests fail, production errors occur, or behavior is flaky.
---

# Systematic debugging

## When to Use

- Intermittent or reproducible bugs
- Failing CI, failing tests, or user-reported errors
- "It works on my machine" situations

## Instructions

1. **Reproduce.** Get exact steps, inputs, versions, and environment. If not reproducible, gather logs, traces, and correlation IDs.
2. **Reduce.** Binary search: disable features, shrink input, bisect git history, isolate with minimal repro.
3. **Hypothesize.** List plausible causes ordered by likelihood; avoid fixing symptoms without confirming root cause.
4. **Instrument.** Add temporary logging or assertions at boundaries (I/O, auth, serialization). Prefer existing observability before new prints.
5. **Verify the fix.** Prove the bug cannot occur with the same trigger; add a regression test when feasible.
6. **Document.** Short note in commit or ticket: cause, fix, and how to detect if it regresses.

## Anti-patterns

- Changing code randomly until something "works"
- Fixing without a repro or without confirming the failure mode
