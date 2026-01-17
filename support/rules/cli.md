# CLI Contract

- List: `opencode-kit list skills|agents|rules`
- Install: `opencode-kit add-skill <name>` / `add-agent <name>`
- Lazy rules base: `opencode-kit add-rules-lazy`
- Rule module: `opencode-kit add-rule <group>/<doc>`

## Strict behaviors

- Copy-only; refuse overwrite.
- `add-rule` errors if `.opencode/rules/_lazy.md` is missing.
- `add-rule` errors if kit module is missing `loader.md` or `rule.md`.
