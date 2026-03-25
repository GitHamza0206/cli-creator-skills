---
name: observability-logging
description: Add structured logging, metrics, and tracing for operability. Use when instrumenting services, debugging production, or defining SLOs.
---

# Observability and logging

## When to Use

- Adding logs to a new service or route
- Improving incident response with better signals
- Defining RED/USE metrics or SLOs

## Instructions

1. **Structured logs.** JSON or key=value fields; stable field names (`level`, `msg`, `service`, `trace_id`, `user_id` where policy allows).
2. **Correlation.** Propagate request/trace IDs across services; include them in error responses (opaque IDs) and logs.
3. **Levels.** `debug` for development volume; `info` for lifecycle; `warn` for recoverable anomalies; `error` for failures needing attention.
4. **Metrics.** Counters for errors and throughput; histograms for latency; gauges for queues or pool usage—aligned with dashboards and alerts.
5. **PII and secrets.** Log minimal identity; redact tokens, passwords, and full card numbers; follow retention policy.
6. **Tracing.** Use spans around outbound calls and critical internal segments when a tracer is available.

## Anti-patterns

- Logging inside tight loops at info level
- Logging entire payloads that may contain secrets
