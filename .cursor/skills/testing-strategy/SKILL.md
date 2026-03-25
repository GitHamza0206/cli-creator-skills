---
name: testing-strategy
description: Plan and implement tests—unit, integration, e2e boundaries, fixtures, and flaky-test mitigation. Use when adding features, fixing bugs, or improving CI reliability.
---

# Testing strategy

## When to Use

- Adding or refactoring tests
- Deciding what to test at which layer
- Debugging flaky CI

## Instructions

1. **Test pyramid.** Prefer fast unit tests for pure logic; integration tests for I/O and DB; fewer e2e tests for critical journeys.
2. **Boundaries.** Test public API and behavior, not private implementation details, unless instability forces narrower tests.
3. **Determinism.** Fix time, randomness, and ordering in tests; avoid real network when a fake or contract test suffices.
4. **Data.** Use factories or fixtures; clean up or isolate state; avoid shared mutable globals between tests.
5. **Regression.** For every bug fix, add a test that fails before the fix when feasible.
6. **Flakes.** Reproduce with repetition; fix root cause (timing, shared state, async) rather than increasing timeouts blindly.

## Checklist

- [ ] Tests fail for the right reason when behavior regresses
- [ ] Critical paths have at least one automated guard
