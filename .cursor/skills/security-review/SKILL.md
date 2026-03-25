---
name: security-review
description: Review code and configuration for common security issues—secrets, injection, authn/authz, and dependencies. Use for security-minded PR review or threat checks.
---

# Security review

## When to Use

- Reviewing code that handles auth, payments, PII, or file uploads
- Auditing configuration (CORS, cookies, headers)
- Assessing dependency or supply-chain risk at a high level

## Instructions

1. **Secrets.** No API keys or tokens in repo, logs, or client bundles. Use env vars or secret managers; rotate if leaked.
2. **Injection.** Parameterize SQL; sanitize/encode for HTML context; avoid shell concatenation; validate and normalize file paths.
3. **Authn and authz.** Verify identity on every protected action; enforce authorization at the server; avoid trusting client-only checks.
4. **Sessions and cookies.** `HttpOnly`, `Secure`, `SameSite` where applicable; CSRF strategy for cookie-based sessions.
5. **Dependencies.** Pin or lock versions; review advisories; minimize install scripts with network side effects.
6. **Headers and CORS.** Least-privilege origins; security headers (CSP, HSTS) when deploying web apps.

## Output

- **Critical / High / Medium / Low** findings with remediation
- Note if full pentest or compliance review is still required
