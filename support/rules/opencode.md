# OpenCode: Rules vs Skills

- `opencode.json -> instructions` are **eagerly loaded** (always-on).
- **Skills** are on-demand (loaded with the `skill` tool).

## Lazy rules pattern (used by this repo)

- Keep `loader.md` always-on and lightweight.
- `loader.md` points to the full rule via:
  - `Load full rule: @rule:.opencode/rules/<group>/<doc>/rule.md`
- The agent reads the referenced `rule.md` only when relevant.
