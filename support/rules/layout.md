# Repo + Module Layout

- CLI: `bin/opencode-kit`
- Kit modules live in: `modules/`
  - Skill: `modules/skill/<name>/SKILL.md`
  - Agent: `modules/agent/<name>.md`
  - Rules: `modules/rules/_lazy.md` and `modules/rules/<group>/<doc>/{loader.md,rule.md}`

## Install destinations (inside a target repo)

- Skills → `.opencode/skill/<name>/SKILL.md`
- Agents → `.opencode/agent/<name>.md`
- Rules → `.opencode/rules/_lazy.md`, plus `.opencode/rules/<group>/<doc>/{loader.md,rule.md}`
