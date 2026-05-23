# Welcome to your Knowlyx workspace 'tutorial'

This folder is your team's **shared brain**. Everything here syncs to GitHub so
every dev (and every AI session) sees the same conventions, decisions, and
approval history.

## What was just created

| File / folder      | Purpose                                                       |
| ------------------ | ------------------------------------------------------------- |
| `workspace.toml`   | Topology — auto-updated when devs link their repos            |
| `skills/`          | Team-authored knowledge files (markdown). See `skills/README.md` |
| `memory.json`      | Decision log — created when you save the first one            |
| `approvals.json`   | Audit trail — created when AI requests its first approval     |

## What to do next

### 1. Push this folder to GitHub (one-time)

```bash
git add .
git commit -m "chore: init knowlyx workspace for tutorial"
git push -u origin main
```

### 2. In each working repo (frontend, backend, etc.), run `knowlyx init`

It will auto-detect this folder as a sibling and link automatically. No flags
needed. The dev only needs to be in the same parent directory as this repo.

### 3. Author your first skill — when you need it

Skills tell the AI things it can't infer from code: UI style, money formatting,
deploy quirks, business rules. Create `skills/<name>.md` with frontmatter:

```markdown
---
name: billing
description: Use when working on payments, orders, or money.
tags: [billing, payments]
---

# Billing rules
- Stripe only, never store raw card data
- Idempotency-Key required on every POST/PUT/DELETE
- Money as string, never JS Number
```

The AI sees skill descriptions via `analyze_intent` and pulls the body via
`read_skill(name)` when relevant. See [skills/README.md](skills/README.md) for
the full format reference.

## Day-to-day workflow

- **Tech lead / anyone**: write skills in `skills/*.md`, commit, push
- **Other devs**: `git pull` in this folder → instantly see updated knowledge
- **Verify Claude actually used Knowlyx**: in any linked repo, run
  ```bash
  knowlyx audit
  ```
  to see which MCP tools the AI called (last ~500 events, capped automatically)

## Useful CLI commands

```bash
knowlyx workspace list             # all registered workspaces on this machine
knowlyx memory list                # all decisions saved (when memory exists)
knowlyx audit                      # AI tool-call log for the current repo
knowlyx init --help                # all init options
```
