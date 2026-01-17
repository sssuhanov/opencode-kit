# opencode-kit

A small, dependency-light **module installer** for OpenCode.

It ships a single CLI (`bin/opencode-kit`) plus a set of modules under `modules/` that can be copied into another project repo.

## Core behavior

- **Copy-only**: copies files into the target repo (no symlinks).
- **Refuse overwrite**: if destination exists → hard error (except: `opencode-kit update`).
- **No auto-edit**: does not automatically edit the target repo’s `AGENTS.md` or `opencode.json`.
- **Manifest**: writes/updates `./.opencode-kit.json` in the target repo root.

## How it chooses the target repo

Run `opencode-kit` while your shell is inside the target project.

- If the directory is a git repo, it installs into the git root (`git rev-parse --show-toplevel`).
- Otherwise, it installs into the current working directory.

## Usage

Use a path to the kit CLI (placeholder):

- `"<path-to-opencode-kit>/bin/opencode-kit" --help`

### List available modules

- `"<path-to-opencode-kit>/bin/opencode-kit" list skills`
- `"<path-to-opencode-kit>/bin/opencode-kit" list agents`
- `"<path-to-opencode-kit>/bin/opencode-kit" list rules`

### Install a skill or agent

- `"<path-to-opencode-kit>/bin/opencode-kit" add-skill <name>`
- `"<path-to-opencode-kit>/bin/opencode-kit" add-agent <name>`

Example agents:

- `security` (read-only checks for secrets/PII/release hygiene)

Installs into the target repo:

- Skills → `.opencode/skill/<name>/SKILL.md`
- Agents → `.opencode/agent/<name>.md`

### Install rules (lazy-loading pattern)

1) Install the lazy loader (required once per target repo):

- `"<path-to-opencode-kit>/bin/opencode-kit" add-rules-lazy`

2) Install a rule module:

- `"<path-to-opencode-kit>/bin/opencode-kit" add-rule <group>/<doc>`

Installs into the target repo:

- `.opencode/rules/_lazy.md`
- `.opencode/rules/<group>/<doc>/loader.md`
- `.opencode/rules/<group>/<doc>/rule.md`

## Enable lazy rules in the target repo (manual)

Because `opencode-kit` does not edit `opencode.json`, you must add the instructions yourself:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [
    ".opencode/rules/_lazy.md",
    ".opencode/rules/**/loader.md"
  ]
}
```

This keeps `loader.md` always-on and loads full `rule.md` only when relevant.

## Manifest (`.opencode-kit.json`)

In the target repo root, `opencode-kit` creates/updates `./.opencode-kit.json` to track:

- What modules were installed (skills/agents/rules/lazy rules base)
- Where they were installed
- When they were installed
- Which module version was installed (`moduleVersion`)

## Update installed modules

- `"<path-to-opencode-kit>/bin/opencode-kit" update`

`update` overwrites only the files previously installed by `opencode-kit` (paths tracked in `.opencode-kit.json`) and refreshes their `moduleVersion`.

## Make it easier to run

Optional: add the kit to your shell `PATH` so you can run `opencode-kit` directly.

## Troubleshooting

- `destination already exists: ...`
  - `opencode-kit` refuses overwrites. Remove/rename the destination manually and retry.
- `missing .opencode/rules/_lazy.md (run: opencode-kit add-rules-lazy)`
  - Install the lazy loader first before `add-rule`.
