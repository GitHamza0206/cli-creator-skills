---
name: cli-design
description: Design command-line interfaces—flags, stdin/stdout conventions, exit codes, and help text. Use when building or reviewing CLIs and scripts. For CLIs driven by AI agents, prefer the cli-for-agents skill.
---

# CLI design

## When to Use

- Creating a new CLI or subcommand
- Standardizing flags and output across tools
- Making scripts safe for CI and humans

**Agent-first CLIs:** When the primary consumer is an AI agent or unattended automation, apply **`cli-for-agents`** in full (non-interactive defaults, examples in every `--help`, idempotency, `--dry-run`, fast-fail errors).

## Instructions

1. **POSIX-style flags.** Short and long forms (`-h`, `--help`); consistent verbs for subcommands (`list`, `get`, `create`).
2. **Stdio contract.** Machine-readable output behind `--json` or when stdout is not a TTY; human tables when interactive; errors to stderr.
3. **Exit codes.** `0` success; non-zero for failure; document meaning for automation (`1` generic, specific codes for known failures if documented).
4. **Defaults and config.** Sensible defaults; config file precedence documented; env vars named clearly (`MYTOOL_API_KEY`).
5. **Help.** Examples in every subcommand’s `--help`; document required permissions and side effects (agents pattern-match on examples).
6. **Safety.** Dry-run or confirm flags for destructive operations; `--yes` / `--force` for automation when confirmations exist; quote paths; avoid shell injection in wrappers.

## Checklist

- [ ] `--help` is accurate and includes examples
- [ ] Scripting use cases work without a TTY
