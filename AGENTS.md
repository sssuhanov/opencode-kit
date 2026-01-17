# AGENTS.md — opencode-kit

This repository is a small, dependency-light "module installer" for OpenCode.
It ships a single CLI (`bin/opencode-kit`) plus a set of Markdown modules under
`modules/` that can be copied into another project.

If anything in a request can be understood two ways, ask a clarifying question.

See also: `ROADMAP.md` (planned work / TODOs).

## Support rules (project-local)

These are not auto-loaded by `opencode.json`.

- `support/rules/goal.md`
- `support/rules/constraints.md`
- `support/rules/layout.md`
- `support/rules/naming.md`
- `support/rules/opencode.md`
- `support/rules/cli.md`
- `support/rules/manifest.md`
- `support/rules/limits.md`

## Cursor/Copilot rules

- No Cursor rules found (`.cursor/rules/`, `.cursorrules`).
- No Copilot instructions found (`.github/copilot-instructions.md`).

## Quick commands (build/lint/test)

This repo currently has **no** package manager config (no `package.json`,
`pyproject.toml`, `go.mod`, etc.) and **no test runner**. The primary “build”
artifact is the executable script itself.

### Run / sanity check

- Show CLI help: `./bin/opencode-kit --help`
- List available modules:
  - Skills: `./bin/opencode-kit list skills`
  - Agents: `./bin/opencode-kit list agents`
  - Rules: `./bin/opencode-kit list rules`

### Lint / formatting (optional but recommended)

There is no repo-pinned tooling; use what is available on your machine.

- Bash syntax check: `bash -n ./bin/opencode-kit`
- ShellCheck (if installed): `shellcheck ./bin/opencode-kit`
- shfmt (if installed): `shfmt -w ./bin/opencode-kit`

### Tests

- There is no test suite yet.
- Preferred direction if you add tests later:
  - Use `bats-core` for Bash tests.
  - Run all: `bats test`
  - Run a single test file: `bats test/opencode-kit.bats`
  - Run a single test case (example): `bats -f "manifest" test/opencode-kit.bats`

## Repo structure

- `bin/opencode-kit`
  - Main CLI entrypoint. Runs in the *target project root* (uses `git rev-parse`
    when available) and writes/updates `./.opencode-kit.json` there.
- `modules/`
  - `modules/skill/<name>/SKILL.md` — skills (on-demand instructions).
  - `modules/agent/<name>.md` — agent presets.
  - `modules/rules/_lazy.md` — global lazy rules loader.
  - `modules/rules/<group>/<doc>/{loader.md,rule.md}` — rule modules.
- `support/rules/`
  - Design constraints and conventions for this repo.
- `ROADMAP.md`
  - Short TODO list / planned features.

## Core behavior and constraints

- **Copy-only**: installer copies files into a target repo; no symlinks.
- **Refuse overwrite**: if destination exists, error out.
- **Do not auto-edit** a target project’s `AGENTS.md` or `opencode.json`.
- **Manifest**: installer creates/updates `./.opencode-kit.json` in the target
  repo to track what was installed and when.

## Naming conventions (repo-specific)

These are enforced by the CLI and should be treated as mandatory.

- Module IDs are **kebab-case**: `^[a-z0-9]+(-[a-z0-9]+)*$`
- Rule modules are addressed as `<group>/<doc>` where both are kebab-case.
- No spaces in module folder names.

## Bash style guidelines (`bin/opencode-kit`)

### General

- Use strict mode at top-level: `set -euo pipefail`.
- Prefer POSIX-ish Bash where possible; keep macOS compatibility in mind.
- Keep functions small and single-purpose.
- Prefer readable, explicit control flow over clever one-liners.

### Quoting and safety

- Quote all variable expansions unless you intentionally want word splitting.
- Use `[[ ... ]]` for tests; avoid `[`.
- Use `local` variables inside functions.
- Validate user input early and fail fast with helpful messages.

### Error handling

- Route user-facing errors through `err`/`die` helpers.
- Include context in failures (what path/argument was invalid).
- Avoid partial writes when possible; if you create directories/files, do so
  in a sequence that leaves the repo in a sensible state on failure.

### External commands

- Assume only baseline tools: `bash`, `git`, `python3`, `mkdir`, `cp`, `ls`.
- Prefer `python3` for JSON manipulation (portable and already used here).
- Avoid adding new hard dependencies unless necessary.

### JSON/manifest

- Treat `./.opencode-kit.json` as append-only-ish state:
  - Update existing keys rather than rewriting unrelated structure.
  - Keep formatting stable (current behavior uses `indent=2` + newline).

## Markdown module guidelines (`modules/**`)

### General

- Keep modules concise and task-focused.
- Prefer clear headings, short bullet lists, and actionable instructions.
- Do not rely on repo-relative links that break when copied into another repo.

### Skills (`modules/skill/*/SKILL.md`)

- Use YAML frontmatter with stable keys:
  - `name`, `description`, `compatibility: opencode`
  - `metadata.domain` / `metadata.scope` when relevant
- Include sections similar to existing skills:
  - “What I do”, “When to use me”, and any workflow constraints.

### Agents (`modules/agent/*.md`)

- Keep frontmatter accurate (`id`, `mode`, `model`, `tools` allowances).
- In the body, state clearly what the agent should focus on.
- Avoid making direct changes unless the agent is designed to do so.

### Rules and lazy loading

- Lazy loader lives at: `modules/rules/_lazy.md`.
- A rule module must include both:
  - `modules/rules/<group>/<doc>/loader.md`
  - `modules/rules/<group>/<doc>/rule.md`
- `loader.md` should be lightweight and include the exact pointer line:
  - `Load full rule: @rule:.opencode/rules/<group>/<doc>/rule.md`
- `rule.md` contains the full instruction set and should be loaded on demand.

## Imports / formatting / types

This repo is Bash + Markdown, so “imports/types” translate to:

- Bash: no implicit globals; pass values via arguments and `local` vars.
- Python snippets (used only as inline one-offs): keep them tiny and embedded
  as here-docs; avoid adding standalone Python modules unless required.
- Formatting:
  - Keep 2-space JSON indentation (matches current manifest writer).
  - Keep Markdown readable; wrap lines reasonably (avoid very long lines).

## Change workflow for agents

- Keep changes minimal and targeted.
- If you touch installer behavior, ensure:
  - Existing commands still work: `./bin/opencode-kit --help`
  - You don’t violate: copy-only, refuse overwrite, no auto-edit of target docs.
- If adding a new module, update nothing outside `modules/` unless necessary.

## Common gotchas

- The CLI changes directory to the *project root* (via `git rev-parse`) before
  writing `.opencode-kit.json`; be careful when assuming paths.
- The `add-rule` command requires `.opencode/rules/_lazy.md` to exist in the
  target repo (installed via `add-rules-lazy`).
