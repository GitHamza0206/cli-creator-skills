# Useful Agent Skills

A collection of [Agent Skills](https://cursor.com/docs/context/skills) for Cursor and other agents that follow the same format. Each skill is a folder with a `SKILL.md` file (YAML frontmatter + instructions).

## Why this repo exists

These skills package repeatable workflows and checklists so agents apply them when the task matches the skill’s `description`. They follow the open [Agent Skills](https://agentskills.io/) pattern: portable, version-controlled, and progressively loaded.

**Note:** The original X post linked as inspiration could not be fetched from this environment (403). Structure and conventions match current Cursor documentation as of 2025.

## Layout

```
.cursor/skills/
├── <skill-name>/
│   ├── SKILL.md          # required
│   ├── scripts/          # optional
│   ├── references/       # optional
│   └── assets/           # optional
```

The `name` field in each `SKILL.md` frontmatter matches the parent folder name.

## Use in Cursor

1. **Clone or submodule** this repo into your project, or copy `.cursor/skills/` into an existing project.
2. **Remote rule:** Cursor Settings → Rules → Add Rule → Remote Rule (GitHub) → paste this repository URL (if your Cursor version supports skill repos that way).
3. **Manual invoke:** Type `/` in Agent chat and search for the skill name.

Skills with `disable-model-invocation: true` in frontmatter only apply when explicitly invoked.

## Skills included

| Skill | Purpose |
|--------|---------|
| `api-design-rest` | REST API design, errors, versioning, pagination |
| `cli-design` | Flags, stdin/stdout, exit codes, help text |
| `code-review` | Structured review: correctness, security, maintainability |
| `debugging-systematic` | Reproduce, isolate, verify fixes |
| `dependency-management` | Upgrades, semver, lockfiles, supply chain |
| `documentation` | READMEs, API docs, inline comments |
| `error-handling` | User-facing errors, logging, recovery |
| `frontend-accessibility` | a11y checks for web UI |
| `git-workflow` | Branches, commits, PR hygiene |
| `internationalization` | Strings, plurals, dates, RTL |
| `mcp-server-design` | MCP tools, auth, schemas, safety |
| `observability-logging` | Structured logs, metrics, tracing |
| `performance` | Measure first, profile, avoid premature optimization |
| `refactoring-safe` | Small steps, tests, behavior preservation |
| `security-review` | Secrets, injection, auth, supply chain |
| `sql-safe` | Parameterized SQL, migrations, least privilege |
| `testing-strategy` | Test pyramid, boundaries, flaky tests |

## Authoring new skills

1. Create `.cursor/skills/<name>/SKILL.md`.
2. Frontmatter: `name` (same as folder), `description` (when to use this skill—agents match on this).
3. Body: **When to Use**, **Instructions**, optional **Anti-patterns** / **Checklist**.

See [Cursor: Agent Skills](https://cursor.com/docs/context/skills) for full field list and examples.

## License

MIT — see [LICENSE](LICENSE).
