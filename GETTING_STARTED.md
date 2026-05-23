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

## Day-to-day workflow — git is automatic

Knowlyx **auto-syncs** every write to the knowledge repo. You usually don't
type `git pull` or `git push` yourself:

- `knowlyx memory decide ...` → save + `git pull --rebase` + `git commit` + `git push`
- `knowlyx approval approve|reject` → same
- `knowlyx init` in a working repo → registers it + pushes the topology update

To opt out (manual git control), set `KNOWLYX_AUTO_SYNC=0` in your environment.

**Manual sync** when you do want it:

```bash
knowlyx sync          # one-shot: pull then push everything pending
knowlyx sync watch    # daemon: pull+push every 60s (Ctrl+C to stop)
knowlyx sync status   # show local vs remote
```

**Verify Claude actually used Knowlyx**: in any linked repo, run

```bash
knowlyx audit
```

to see which MCP tools the AI called (last ~500 events, capped automatically).

## Useful CLI commands

```bash
knowlyx workspace list             # all registered workspaces on this machine
knowlyx memory list                # all decisions saved (when memory exists)
knowlyx audit                      # AI tool-call log for the current repo
knowlyx init --help                # all init options
```
