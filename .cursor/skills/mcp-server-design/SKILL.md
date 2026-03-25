---
name: mcp-server-design
description: Design or review MCP (Model Context Protocol) servers—tools, resources, prompts, auth, and error surfaces. Use when building or extending MCP integrations.
---

# MCP server design

## When to Use

- Implementing a new MCP server or tool surface
- Reviewing tool schemas and safety boundaries
- Exposing databases, APIs, or internal systems to agents

## Instructions

1. **Minimize capability surface.** Expose the smallest set of tools needed; prefer read-only tools until requirements demand writes.
2. **Clear tool contracts.** Precise names, descriptions, and JSON schemas so models invoke tools correctly. Document required vs optional args and units (seconds, bytes, IDs).
3. **Auth and tenancy.** Never rely on client-side identity; validate tokens or keys on every call; scope data to the authenticated principal.
4. **Side effects.** Label destructive operations explicitly; require confirmation patterns at the product layer when appropriate; implement idempotency for risky writes.
5. **Errors.** Return structured errors the agent can reason about; include safe hints, not internal stack traces, in user-visible paths.
6. **Rate limits and cost.** Protect upstream APIs and databases; stream or paginate large results; set timeouts on outbound calls.

## Checklist

- [ ] Tools are documented with examples of valid input
- [ ] Secrets are not passed through tool arguments when headers or server config suffice
