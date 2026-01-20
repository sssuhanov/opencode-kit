# CLI Contract

- List: `opencode-kit list modules`
- Init OpenCode config: `opencode-kit init`
- Install: `opencode-kit add-module <group>/<module>`
- Update installed modules: `opencode-kit update`

## Strict behaviors

- Copy-only; refuse overwrite (except: `update` overwrites manifest-tracked files).
- Installer never edits target `AGENTS.md`; `opencode-kit init` may create/update `opencode.json` when explicitly run.
- Manifest schema is version 2 (module-based); older manifests are not supported.
