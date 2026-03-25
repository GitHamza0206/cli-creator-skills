---
name: performance
description: Improve performance using measurement, profiling, and targeted fixes. Use when the user reports slowness, high CPU/memory, or scaling concerns.
---

# Performance

## When to Use

- Latency or throughput problems in apps or APIs
- High memory usage or CPU hotspots
- Database or N+1 query issues

## Instructions

1. **Measure first.** Establish a baseline with metrics, traces, or profilers. Define the SLO or acceptable latency before optimizing.
2. **Find the bottleneck.** CPU vs I/O vs lock contention vs network; use flame graphs, query plans, or APM as appropriate.
3. **Fix the largest cost.** Avoid micro-optimizations until hot paths are addressed.
4. **Caching.** Add caches only with clear invalidation strategy; watch stale data and memory bounds.
5. **Algorithms and data structures.** Prefer better complexity when data size warrants it; batch work and reduce round trips.
6. **Verify.** Re-measure after changes; guard against regressions with a benchmark or metric where practical.

## Anti-patterns

- Optimizing without profiling
- Caching without a defined TTL or invalidation story
