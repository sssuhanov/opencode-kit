# Core Constraints

- **Copy-only**: never symlink.
- **Refuse overwrite**: if destination exists → hard error (except: `opencode-kit update`).
- **Do not auto-edit** a target repo’s `AGENTS.md` or `opencode.json`.
- Prefer baseline tools only (`bash`, `git`, `python3`, `mkdir`, `cp`, `ls`).
