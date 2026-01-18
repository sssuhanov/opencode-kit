# CLI Contract

- List: `opencode-kit list modules`
- Install: `opencode-kit add-module <group>/<module>`
- Update installed modules: `opencode-kit update`

## Strict behaviors

- Copy-only; refuse overwrite (except: `update` overwrites manifest-tracked files).
- Installer never edits target `AGENTS.md` or `opencode.json`.
- Manifest schema is version 2 (module-based); older manifests are not supported.
