# Per-project Manifest

- The installer creates/updates: `./.opencode-kit.json` (in the target repo root).
- It records what was installed (modules).
- It records installed module versions (`moduleVersion`) from each module’s `MODULE.md`.
- Treat it as “append-only-ish”: update existing keys; avoid rewriting unrelated structure.
