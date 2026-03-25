---
name: cli-for-agents
description: Build CLIs that AI agents can run—non-interactive flags, progressive discovery, subcommand help with examples, stdin and pipelines, fast actionable errors, idempotency, dry-run, --yes or --force, predictable noun-verb structure, and factual success output. Use when implementing, reviewing, or refactoring CLIs for agents, CI, or automation.
metadata:
  source: Building CLIs for agents — Eric Zakariasson
  reference: https://x.com/ericzakariasson/status/2036762680401223946
---

# Building CLIs for agents

Human-oriented CLIs block agents: interactive prompts, walls of docs, help without examples. Design CLIs so **every input is explicit**, **help is discovered in layers**, and **automation can recover from mistakes**.

## When to Use

- Implementing a new CLI or subcommand that agents or scripts will run
- Auditing an existing CLI for blocking prompts, weak `--help`, or non-idempotent side effects
- Adding flags so interactive-only flows become scriptable

## Core principles (from the article)

### 1. Non-interactive first

If the CLI drops into a prompt mid-run, an agent is stuck (no arrow keys, no timely “y”). **Every input must be passable as a flag** (or equivalent non-interactive channel). Interactive mode is a **fallback** when flags are missing—not the primary path.

```bash
# blocks an agent
$ mycli deploy
? Which environment? (use arrow keys)

# works
$ mycli deploy --env staging
```

### 2. Progressive documentation

Do **not** dump the full manual up front. Agents discover: run `mycli`, see subcommands, run `mycli deploy --help`, get what they need. **No wasted context** on commands they will not use.

### 3. `--help` that works (examples do the teaching)

**Every subcommand** has `--help`. **Every `--help` includes examples.** Agents pattern-match from invocations faster than from long descriptions.

```bash
$ mycli deploy --help
Options:
  --env     Target environment (staging, production)
  --tag     Image tag (default: latest)
  --force   Skip confirmation

Examples:
  mycli deploy --env staging
  mycli deploy --env production --tag v1.2.3
  mycli deploy --env staging --force
```

### 4. Flags and stdin for everything (pipelines)

Agents think in **pipelines**. Support **chaining** and **pipes**. Avoid weird positional ordering and **do not** fall back to interactive prompts for missing values.

```bash
cat config.json | mycli config import --stdin
mycli deploy --env staging --tag $(mycli build --output tag-only)
```

### 5. Fail fast with actionable errors

If a required flag is missing, **do not hang**. Exit immediately and show the **correct invocation**. Agents self-correct when given something concrete to run.

```bash
Error: No image tag specified.
  mycli deploy --env staging --tag <image-tag>
  Available tags: mycli build list --output tags
```

### 6. Idempotent commands

Agents **retry constantly** (timeouts, lost context). Running the same command twice should yield **“already done” / no-op**, not duplicates.

### 7. `--dry-run` for destructive actions

Let agents **preview** deploys, deletes, or other risky operations, then run for real after validating the plan.

```bash
$ mycli deploy --env production --tag v1.2.3 --dry-run
Would deploy v1.2.3 to production
  - Stop 3 running instances
  - Pull image registry.io/app:v1.2.3
  - Start 3 new instances
No changes made.

$ mycli deploy --env production --tag v1.2.3
✓ Deployed v1.2.3 to production
```

### 8. `--yes` / `--force` to skip confirmations

Humans get “are you sure?”; agents pass **`--yes`** (or your documented bypass). Keep the **safe default** for humans; allow **explicit** non-interactive override for automation.

### 9. Predictable command structure

If an agent learns `mycli service list`, it should infer `mycli deploy list`, `mycli config list`. Pick **one pattern** (e.g. **resource + verb**) and use it **everywhere**.

### 10. Return data on success

Show what matters next: **deploy ID**, **URL**, **identifiers**, **duration**. Decorative output is optional; **facts** are not.

```bash
deployed v1.2.3 to staging
url: https://staging.myapp.com
deploy_id: dep_abc123
duration: 34s
```

## Implementation checklist

- [ ] Happy paths run with **zero prompts** when flags/env/stdin provide required input
- [ ] Each subcommand’s `--help` ends with **copy-paste examples**
- [ ] Missing required input → **immediate exit**, stderr message, **suggested command** (and list/discover commands if helpful)
- [ ] Destructive or state-changing commands are **idempotent** or clearly **single-shot** with safe retry behavior documented
- [ ] Risky commands support **`--dry-run`** (or equivalent) with a clear plan summary
- [ ] Confirmations can be skipped with **`--yes`** / **`--force`** (documented, not hidden)
- [ ] Command tree follows a **single naming pattern** across the CLI
- [ ] Success output includes **stable, parse-friendly** facts (IDs, URLs, paths, durations)

## Anti-patterns (agent breakers)

- Arrow-key or mid-flight prompts as the only way to supply required data
- Global help that lists everything with no path to **per-subcommand** `--help` + examples
- Hanging or defaulting silently when input is missing
- Duplicate resources on identical repeated invocations (unless explicitly documented as “run each time”)

## Optional deep dive

For the full article prose and context, see `references/BUILDING-CLIS-FOR-AGENTS.md` in this skill folder (load only when the user asks for the original wording or attribution details).
