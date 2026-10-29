# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal collection of Claude Code skills (Markdown + static assets). No build, lint, or test tooling — "running" a skill means installing it and invoking it from Claude Code. Docs and skill content are mostly in Korean; keep that language when editing.

## Install

Skills are installed by symlinking a skill directory into `~/.claude/skills/`:

```sh
ln -s "$PWD/skills/editorial-slide-deck" ~/.claude/skills/
```

Enable the pre-commit hook (checks `SKILL.md` frontmatter) once per clone:

```sh
git config core.hooksPath .githooks
```

`skills/engineering/` is a grouping folder, not a skill — symlink its subdirectories (`diagnose`, `grill-with-docs`, `to-prd`) individually.

## Layout

- `skills/<name>/SKILL.md` — frontmatter `name` + `description` (the description is the trigger condition), then instructions. Optional `references/` (read on demand) and `assets/` (templates).
- `prompt/` — example prompts for invoking skills, not skills themselves.
- `private/` — gitignored working output (generated decks etc.). Don't commit.

## Skill-specific notes

- **editorial-slide-deck**: generated decks copy `assets/slide-template.html` and replace only the `<section class="slide">` elements; template CSS/JS is not modified per deck. Visual rules live in `references/design-system.md`. The template's example slides double as component usage docs.
- **wbs**: `SKILL.md` is the WBS authoring guide; `wbs.html` is the reference output.
- **engineering/**: adapted from https://github.com/mattpocock/skills. `to-prd` assumes the upstream `/setup-matt-pocock-skills` configuration.

## Adding a skill

1. Create `skills/<name>/SKILL.md` with `name`/`description` frontmatter.
2. Add a row to the skill table in `README.md`.
