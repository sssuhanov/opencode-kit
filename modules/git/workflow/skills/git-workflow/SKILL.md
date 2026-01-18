---
name: git-workflow
description: Mandatory Git workflow for any project file changes (branch, test checklist, commit, optional merge).
compatibility: opencode
version: 1.0.1
metadata:
  domain: git
  scope: workflow
---

## What I do

- Enforce a mandatory Git workflow whenever the agent is about to change any files in a project.
- Require a new branch, project-specific testing, a clean commit, and explicit user approval for merging.
- Keep actions safe and local by default (no push/PR unless the user explicitly asks).

## When to use me

- Use me every time you are going to modify any project files (code, configs, docs, CI, etc.).
- Use me before refactors, bug fixes, feature work, and any non-trivial edits.

## Required workflow (must follow in order)

### 0) Preconditions

- If the project is not a git repo, stop and ask the user how to proceed.
- Before doing anything, ask the user to confirm you should apply file changes.

### 1) Check current state

- Run `git status`.
- If there are existing changes (dirty working tree), ask what to do.
  - Default recommendation: stash them.
  - Offer options:
    - Stash: `git stash push -u -m "wip before <topic>"`
    - Commit them first (only if the user wants)
    - Discard (only with explicit user permission)

### 2) Decide base branch

- Detect the default branch (do not assume `main`).
  - Use whatever is available (examples):
    - `git remote show origin` (if `origin` exists)
    - or list local branches and ask
- Ask the user which base branch to start from.
- Ask whether to run `git pull` to update it.
  - Do not do any remote/network action unless the user explicitly approves.

### 3) Create and checkout a new branch

- Ask the user for a branch name.
- Create and checkout it:
  - `git checkout -b <branch>`

### 4) Change files

- Apply the required edits.
- Keep changes minimal and focused.

### 5) Test the changes (ask first)

- Propose a generic checklist and ask: “Do you want me to run these on this branch now?”
- The checklist is generic; ask the user for the exact commands used in this project.

**Suggested checklist (smallest → biggest):**

- Format (if configured): e.g. `prettier`, `black`, `gofmt`, `rustfmt`
- Lint (if configured): e.g. `eslint`, `ruff`, `golangci-lint`, `shellcheck`
- Typecheck (if relevant): e.g. `tsc -p .`, `mypy`
- Unit tests: e.g. `pytest`, `go test ./...`, `npm test`
- Build/compile: e.g. `npm run build`, `go build ./...`, `cargo build`
- Integration/e2e tests (if present): e.g. `playwright test`, `cypress run`

**If the repo has no tests/commands configured:**

- Ask the user what “minimal check” means for this project.
- If the user agrees, run the minimal check and then ask if more checks are needed.

**Failure policy:**

- If any test/check fails, stop and ask the user what to do next (fix now, change scope, or stop).

### 6) Commit the changes

- Ensure the working tree contains only intended changes (`git status`).
- Ask the user for a commit message appropriate to what changed.
- Create the commit.

### 7) Merge (only if user allows)

- Ask the user:
  - whether to merge at all
  - which target branch to merge into
- Merge using a merge commit (keep history of the feature branch).
  - Example: `git checkout <target>` then `git merge --no-ff <branch>`
- Do not push/open PR unless the user explicitly asks.

### 8) Cleanup (ask first)

- Ask whether to delete the branch.
- Delete only if the user approves.
