---
name: api-design-rest
description: Design or refactor REST HTTP APIs—resources, status codes, errors, versioning, pagination, and idempotency. Use when building or reviewing APIs, OpenAPI specs, or backend routes.
---

# REST API design

## When to Use

- Designing new HTTP APIs or extending existing ones
- Reviewing route shapes, status codes, or error payloads
- Writing or updating OpenAPI/Swagger specs

## Instructions

1. **Model resources, not actions.** Prefer nouns and collections (`/users`, `/users/{id}`); use HTTP verbs for operations. Avoid RPC-style paths unless the product standard requires them.
2. **Use appropriate status codes.** `200`/`201`/`204` for success; `400` for client mistakes; `401` vs `403` deliberately; `404` when the resource identity is unknown to the caller; `409` for conflicts; `422` for semantic validation; `429` with rate-limit headers when throttling; `5xx` only for true server failures.
3. **Consistent error body.** One JSON shape across endpoints (e.g. `code`, `message`, optional `details`, `request_id`). Never leak stack traces or secrets in production responses.
4. **Versioning.** Prefer URL prefix (`/v1/...`) or clear deprecation headers; document breaking vs non-breaking changes.
5. **Pagination and filtering.** Use cursor or offset/limit consistently; document max limits. Prefer stable sort keys for cursor pagination.
6. **Idempotency.** Use `Idempotency-Key` (or equivalent) for unsafe retries on payments and creates where duplicates are costly.
7. **Security defaults.** HTTPS, authentication on mutating routes, input validation, rate limits for auth and expensive operations.

## Checklist

- [ ] Resource names are plural and consistent
- [ ] Errors are machine-readable and logged with correlation IDs
- [ ] Breaking changes are versioned or deprecated with a timeline
