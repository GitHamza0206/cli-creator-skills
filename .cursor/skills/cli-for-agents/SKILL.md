---
name: cli-for-agents
description: Build CLIs that AI agents can run reliably—non-interactive flags, progressive discovery, examples in --help, stdin and pipelines, fast-fail errors, idempotency, dry-run, and --yes. Use when designing or reviewing CLIs meant for agents, CI, or automation.
metadata:
  inspired_by: Building CLIs for agents (Eric Zakariasson)
---

# CLIs for agents

Most CLIs assume a human at the keyboard. Agents get stuck on interactive prompts, empty help, or ambiguous errors. Design so every input is explicit and discoverable.

## When to Use

- Designing a new CLI or subcommand that agents or scripts will call
- Reviewing a CLI for “works in terminal but breaks for automation” issues
- Adding flags so existing interactive flows become scriptable

## Instructions

1. **Non-interactive by default.** Never block on arrow-key menus or mid-run prompts agents cannot answer. Every value should be passable as a flag (or env). Keep TTY/interactive mode only as a **fallback** when flags are missing—not the primary path.

   ```bash
   # blocks an agent
   mycli deploy
   # ? Which environment? (use arrow keys)

   # works
   mycli deploy --env staging
   ```

2. **Progressive documentation.** Do not dump the full manual on first run. Agents discover: `mycli` → subcommands → `mycli deploy --help`. Let them pull only what they need.

3. **`--help` must include examples.** Every subcommand gets `--help`. Examples do most of the work; agents pattern-match faster from `mycli deploy --env staging --tag v1.2.3` than from prose alone. List options, defaults, then **Examples:** with copy-paste invocations.

4. **Flags and stdin for inputs.** Support pipelines and composition. Avoid odd positional ordering and avoid falling back to interactive prompts for missing values.

   ```bash
   cat config.json | mycli config import --stdin
   mycli deploy --env staging --tag "$(mycli build --output tag-only)"
   ```

5. **Fail fast with actionable errors.** If a required flag is missing, exit immediately with a suggested command (and pointers to list commands if useful).

   ```text
   Error: No image tag specified.
     mycli deploy --env staging --tag <image-tag>
     Available tags: mycli build list --output tags
   ```

6. **Idempotent commands.** Agents retry often (timeouts, lost context). Running the same deploy twice should be a no-op or clearly report “already done,” not create duplicates.

7. **`--dry-run` for destructive work.** Let agents preview deploys, deletes, or migrations, then run without `--dry-run` after validating the plan. Summarize what would change; make “no changes made” obvious.

8. **`--yes` / `--force` for confirmations.** Humans get “are you sure?”; agents pass `--yes` (or documented equivalent). Keep the safe default for humans; document the bypass for automation.

9. **Predictable structure.** If `mycli service list` exists, agents infer `mycli deploy list`, `mycli config list`. Pick one pattern (e.g. resource + verb) and use it consistently.

10. **Useful success output.** On success, print machine-relevant facts: IDs, URLs, primary artifact names, duration. Minimize decorative output; plain key-value or structured lines are easier to parse and chain.

    ```text
    deployed v1.2.3 to staging
    url: https://staging.myapp.com
    deploy_id: dep_abc123
    duration: 34s
    ```

## Anti-patterns

- Interactive wizards as the only way to supply required data
- `--help` with options but no examples
- Hanging or prompting instead of exiting with a fix suggestion
- Non-idempotent side effects on repeated identical invocations

## Checklist

- [ ] Full flows work with zero prompts when flags/env are provided
- [ ] Each subcommand’s `--help` ends with concrete examples
- [ ] Destructive commands support `--dry-run` and documented non-interactive confirm bypass
- [ ] Missing required input yields immediate stderr + suggested invocation
