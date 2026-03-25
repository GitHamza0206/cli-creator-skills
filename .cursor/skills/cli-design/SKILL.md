---
name: cli-design
description: Design command-line interfaces—flags, stdin/stdout conventions, exit codes, and help text. Use when building or reviewing CLIs and scripts.
---

# CLI design

## When to Use

- Creating a new CLI or subcommand
- Standardizing flags and output across tools
- Making scripts safe for CI and humans

## Instructions

1. **POSIX-style flags.** Short and long forms (`-h`, `--help`); consistent verbs for subcommands (`list`, `get`, `create`).
2. **Stdio contract.** Machine-readable output behind `--json` or when stdout is not a TTY; human tables when interactive; errors to stderr.
3. **Exit codes.** `0` success; non-zero for failure; document meaning for automation (`1` generic, specific codes for known failures if documented).
4. **Defaults and config.** Sensible defaults; config file precedence documented; env vars named clearly (`MYTOOL_API_KEY`).
5. **Help.** Examples in `--help`; document required permissions and side effects.
6. **Safety.** Dry-run or confirm flags for destructive operations; quote paths; avoid shell injection in wrappers.

## Checklist

- [ ] `--help` is accurate and includes examples
- [ ] Scripting use cases work without a TTY
