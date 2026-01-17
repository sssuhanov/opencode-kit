# Per-project Manifest

- The installer creates/updates: `./.opencode-kit.json` (in the target repo root).
- It records what was installed (skills/agents/rules/lazy rules base).
- It records installed module versions (`moduleVersion`).
- Treat it as “append-only-ish”: update existing keys; avoid rewriting unrelated structure.
