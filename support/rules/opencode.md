# OpenCode: Rules vs Skills

- `opencode.json -> instructions` are **eagerly loaded** (always-on).
- **Skills** are on-demand (loaded with the `skill` tool).

## Rules

- Rules are instruction docs meant to be included in `opencode.json -> instructions`.
- Since instructions are eagerly loaded, keep rules concise and task-focused.
- If a module needs a custom “load only when relevant” workflow, document that behavior inside the module’s rule docs.
