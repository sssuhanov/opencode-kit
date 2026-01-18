---
version: 1.0.0
---

# Working with Obsidian vaults

These are general rules for editing an Obsidian vault safely.

## Safety first

- Avoid breaking internal links: rename/move notes using Obsidian when possible.
- Be careful with mass edits and path changes; verify backlinks after changes.
- Avoid editing `.obsidian/` unless the user explicitly asks.

## Markdown and frontmatter

- Keep YAML frontmatter valid (no tabs, consistent indentation).
- Prefer simple, readable Markdown; avoid exotic syntax unless needed.

## Plugins and rendering

- If you add/update snippets for plugins (Templater/Dataview/Tasks), ask the user
  how they want to verify it inside Obsidian.
- Don’t assume a specific plugin configuration exists; treat paths/config as
  user-provided unless present in the repo.

## Reference

- Obsidian docs: https://help.obsidian.md
