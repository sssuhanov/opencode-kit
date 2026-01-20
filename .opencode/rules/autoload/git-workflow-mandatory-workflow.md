---
version: 1.0.0
autoload: true
---

# Mandatory Git workflow (use `git-workflow` skill)

Before making any file changes (create/edit/delete/move/rename) in a project, you MUST load and follow the `git-workflow` skill.

## How to comply

- Load the skill using the `skill` tool: `git-workflow`.
- Follow the workflow steps from the skill (branch, checks/tests, commit, optional merge).

## User override (allowed, but explicit)

- If the user explicitly tells you to proceed without this workflow, you may skip it.
- Before skipping, restate what will be skipped (branch discipline, checks/tests, clean commit, merge safety) and ask for confirmation.
- If confirmed, proceed with minimal, focused changes and call out the increased risk.

## What this module provides

- Skill ID: `git-workflow`
- Purpose: mandatory Git workflow whenever changing project files.
