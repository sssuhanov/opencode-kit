---
name: module-versioning
description: Policy for opencode-kit: bump module versions whenever modules/ change so opencode-kit update can propagate.
compatibility: opencode
metadata:
  repo: opencode-kit
  topic: versioning
---

## What I do

- Enforce a simple rule: if you change anything under `modules/**`, you must bump that module file’s frontmatter `version:` (semver).
- Explain how `opencode-kit update` decides whether to update installed files.

## Why this matters

`opencode-kit update` overwrites previously-installed files only when the kit module version is greater than the installed `moduleVersion` in the target repo’s `.opencode-kit.json`.

If you change module content but forget to bump `version:`, target repos will stay “up-to-date” and won’t receive the change.

## Version bump guidelines

- Patch (`x.y.Z`): typo fixes, wording changes, small clarifications.
- Minor (`x.Y.0`): behavioral tightening/loosening, new restrictions, compatible improvements.
- Major (`X.0.0`): breaking behavior changes or rework that could surprise users.

## Scope

- Bump versions only in `modules/**` when changing kit modules.
- Treat `.opencode/**` as project-local runtime config; don’t “sync” versions there manually unless you intentionally want to change this repo’s local OpenCode behavior.
