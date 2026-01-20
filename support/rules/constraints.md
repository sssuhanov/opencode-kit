# Core Constraints

- **Copy-only**: never symlink.
- **Refuse overwrite**: if destination exists → hard error (except: `opencode-kit update`).
- **Do not auto-edit** a target repo’s `AGENTS.md`; `opencode-kit init` may create/update `opencode.json` when explicitly run.
- Prefer baseline tools only (`bash`, `git`, `python3`, `mkdir`, `cp`, `ls`).
