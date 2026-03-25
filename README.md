# CLI skills for agents

This repository is a **single [Agent Skill](https://cursor.com/docs/context/skills)**: guidance for building command-line tools that **AI agents** (and CI) can run reliably.

It follows Eric Zakariasson’s *Building CLIs for agents* — [post on X](https://x.com/ericzakariasson/status/2036762680401223946). The skill distills that article into actionable rules; the original prose lives under `references/` for optional reading.

## What’s inside

```
.cursor/skills/cli-for-agents/
├── SKILL.md                              # what agents load first
└── references/
    └── BUILDING-CLIS-FOR-AGENTS.md       # full article text (reference)
```

## Guidelines (summary)

| Topic | Rule |
|--------|------|
| Input | **Non-interactive first** — every value via flags (or stdin/env); interactive only as fallback |
| Docs | **Progressive discovery** — no doc dump; `tool` → subcommand → `tool cmd --help` |
| Help | **Examples on every subcommand `--help`** — pattern-matching beats prose |
| Pipes | **Flags + stdin** — support pipelines; no odd positional-only flows |
| Errors | **Fail fast** — suggest the exact fix / next command |
| Retries | **Idempotent** where it matters — safe when agents rerun |
| Risk | **`--dry-run`** — show plan, then run for real |
| Confirm | **`--yes` / `--force`** — documented bypass for automation |
| Shape | **One pattern** (e.g. resource + verb) everywhere |
| Success | **Facts** — IDs, URLs, duration; minimal decoration |

## Use in Cursor

1. Copy `.cursor/skills/cli-for-agents` into your project’s `.cursor/skills/`, or add this repo as a remote rule if your Cursor version supports it (Settings → Rules).
2. Invoke **`/cli-for-agents`** when you want the full skill in context, or let the agent pick it up from the `description` when you’re building or reviewing a CLI.

## License

MIT — see [LICENSE](LICENSE).
