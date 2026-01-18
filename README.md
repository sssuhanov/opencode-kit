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

- `"<path-to-opencode-kit>/bin/opencode-kit" list modules`

### Install a module

- `"<path-to-opencode-kit>/bin/opencode-kit" add-module <group>/<module>`

Installs into the target repo:

- Agents → `.opencode/agent/<group>-<module>-<doc>.md`
- Skills → `.opencode/skill/<skill-id>/SKILL.md`
- Rules → `.opencode/rules/<group>-<module>-<doc>.md`

## Manifest (`.opencode-kit.json`)

In the target repo root, `opencode-kit` creates/updates `./.opencode-kit.json` (schema version 2) to track:

- Which modules were installed
- Exactly which files were installed (`src`/`dst` mapping)
- When they were installed
- Which module version was installed (`moduleVersion`, read from `MODULE.md`)

## Update installed modules

- `"<path-to-opencode-kit>/bin/opencode-kit" update`

`update` overwrites only the files previously installed by `opencode-kit` (as tracked in `.opencode-kit.json`) when the kit’s `MODULE.md` version is newer.

## Make it easier to run

Optional: add the kit to your shell `PATH` so you can run `opencode-kit` directly.

## Troubleshooting

- `destination already exists: ...`
  - `opencode-kit` refuses overwrites. Remove/rename the destination manually and retry.
- `unsupported manifest version: ...`
  - This repo no longer supports legacy manifests. Delete `.opencode-kit.json` in the target repo and reinstall modules.
