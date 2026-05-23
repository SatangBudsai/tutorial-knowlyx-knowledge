# Skills — team-authored knowledge

Drop `<name>.md` files here. Each file is a "skill" — a piece of knowledge
the AI should consult when working in a related area (UI style, money
formatting, deploy quirks, anything that isn't obvious from the code).

## File format

```markdown
---
name: ui-style
description: Use when building or editing UI components — covers Tailwind, design tokens, and shared components.
tags: [ui, frontend]
---

# UI Style Guide

- Use Tailwind v4 utility classes; no inline `style={}`
- Money: format as `THB X,XXX.XX`
- All buttons must use `<Button>` from `src/components/ui/Button.tsx`
- Dark mode: respect `prefers-color-scheme`
```

## How the AI uses them

1. `analyze_intent` returns `available_skills` (every skill's name + description)
2. The AI scans descriptions and calls `read_skill(name)` on anything relevant
3. The AI follows the skill's guidance when writing code

## Authoring tips

- Keep descriptions specific — they're how the AI decides relevance
- Body is free markdown — lists, code blocks, examples all welcome
- Commit + push: skills live in the knowledge repo and sync with the team
