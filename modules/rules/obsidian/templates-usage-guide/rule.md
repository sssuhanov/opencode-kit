# Obsidian templates (general)

Guidance for working with templates in Obsidian vaults.

## Template strategies

- **Manual templates**: user triggers a template insertion command when creating
  a note.
- **Folder-mapped templates** (common with Templater): templates apply
  automatically based on the folder.

## What to verify

- Where templates are stored (often a dedicated `Templates/` folder).
- Whether folder mappings exist (if using Templater, mappings may live under
  `.obsidian/plugins/templater-obsidian/`).
- Whether any dashboards/queries depend on specific folder paths.

## Safe changes

- Ask before changing template mappings or moving template files.
- When changing a template, check whether existing notes depend on the old field
  names (including typos that are "part of the schema").
