---
name: error-handling
description: Design consistent error handling—user-facing messages, logging, retries, and recovery. Use when implementing APIs, CLIs, workers, or UI error states.
---

# Error handling

## When to Use

- Implementing try/catch, Result types, or error middleware
- Unifying error responses or toast messages
- Designing retry and backoff for I/O

## Instructions

1. **Classify errors.** Distinguish user errors (invalid input), system errors (dependency down), and programmer errors (bugs). Handle each class differently.
2. **User-facing text.** Clear, non-accusatory, actionable where possible. Map internal codes to safe messages; log rich context server-side only.
3. **Logging.** Structured logs with correlation/request IDs; log stack traces for unexpected errors, not for expected validation failures.
4. **Retries.** Retry only idempotent or safely retried operations; use exponential backoff and jitter; respect `Retry-After` when present.
5. **Partial failure.** In batch jobs, prefer per-item errors over failing the whole batch when the domain allows.
6. **Never swallow errors silently.** If intentionally ignored, comment why and scope narrowly.

## Checklist

- [ ] Sensitive data is not logged or returned to clients
- [ ] Callers can distinguish retryable vs permanent failures
