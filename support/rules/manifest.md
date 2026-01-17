# Per-project Manifest

- The installer creates/updates: `./.opencode-kit.json` (in the target repo root).
- It records what was installed (skills/agents/rules/lazy rules base).
- Treat it as “append-only-ish”: update existing keys; avoid rewriting unrelated structure.
