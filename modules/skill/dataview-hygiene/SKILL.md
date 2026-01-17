---
name: dataview-hygiene
description: Checklist for writing and validating Dataview queries in this vault without breaking dashboards.
compatibility: opencode
metadata:
  domain: obsidian
  scope: dataview
---

## What I do

- Validate that Dataview `FROM` values match real folder paths.
- Flag likely causes of empty results: wrong folder name, mismatched tags, missing YAML fields.
- Recommend safe validation steps inside Obsidian (open the note and confirm render/backlinks).

## When to use me

- Before adding or changing Dataview blocks.
- When a dashboard renders empty unexpectedly.

## Known gotcha (document-only)

- Some dashboards/notes use `FROM "Meeting"`, but meetings live in `5 Support/Meeting/`.
  - Result: those Dataview queries may return empty until adjusted.
