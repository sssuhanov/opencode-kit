---
version: 1.0.0
---

# OpenCode (skills, agents, rules)

Use this as general guidance for working with OpenCode configuration and its
instruction building blocks.

## Concepts

- **Rules**: instruction files loaded via `opencode.json -> instructions` (always-on).
- **Skills**: on-demand instruction packs loaded via the `skill` tool.
- **Agents**: presets that constrain behavior/tools.

## Skills (recommended for reusable, on-demand guidance)

- Location (project-scoped): `.opencode/skill/<name>/SKILL.md`
- Each skill lives in its own folder and contains a single `SKILL.md`.
- Skill naming must be kebab-case: `^[a-z0-9]+(-[a-z0-9]+)*$`.

## Rules (always-on instructions)

- Prefer small “selector” rules + optional full rules (lazy load pattern).
- If using lazy rules, keep `loader.md` lightweight and point to a full `rule.md`.

## Working principles

- Ask before making file changes unless the user explicitly requested them.
- Prefer minimal, portable setups (avoid project-specific assumptions).
- When in doubt, show the exact file(s) you intend to touch and why.
