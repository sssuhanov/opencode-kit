# Repo + Module Layout

- CLI: `bin/opencode-kit`
- Kit modules live in: `modules/`
  - Module: `modules/<group>/<module>/MODULE.md`
  - Agents: `modules/<group>/<module>/agents/<doc>.md`
  - Skills: `modules/<group>/<module>/skills/<skill-id>/SKILL.md`
  - Rules: `modules/<group>/<module>/rules/<doc>.md`

## Install destinations (inside a target repo)

- Agents → `.opencode/agent/<group>-<module>-<doc>.md`
- Skills → `.opencode/skill/<skill-id>/SKILL.md`
- Rules → `.opencode/rules/<group>-<module>-<doc>.md`
