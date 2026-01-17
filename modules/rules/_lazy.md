# Lazy Rules Loader

These instructions define how to use rule modules stored under `.opencode/rules/`.

## What to load automatically

- Treat all files matching `.opencode/rules/**/loader.md` as always-on, lightweight selectors.
- Do not automatically load `.opencode/rules/**/rule.md` files.

## Lazy loading mechanism

If a `loader.md` contains a pointer like:

- `Load full rule: @rule:.opencode/rules/<group>/<doc>/rule.md`

Then:

- Only load (`read`) that referenced `rule.md` if it is relevant to the current user task.
- If relevant, load it immediately and follow it as mandatory instructions.
- Do not mass-load all rule files; load the minimum needed.

## Precedence

- If a loaded `rule.md` conflicts with generic guidance, follow the `rule.md` for the current task.
