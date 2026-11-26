---
name: project-setup
description: Scaffold a new project's skeleton (folders, AGENTS.md, CLAUDE.md, glossary.md, .gitignore, the ADR and tracker templates, the skills symlinks). Run once per project, before project-grilling.
disable-model-invocation: true
---

# Project setup

Scaffold the skeleton every other `project-*` skill assumes, by copying the templates in `templates/`. Each template mirrors its path in the project.

## Language and naming

- Talk to the user in Indonesian. Every file written into the project is in Indonesian.
- File and folder names are lowercase kebab-case, except `AGENTS.md`, `CLAUDE.md`, `SKILL.md`, `README.md`, `LICENSE`.

## Skeleton

| Project path | Source |
|---|---|
| `AGENTS.md` | `templates/AGENTS.md` |
| `CLAUDE.md` | `templates/CLAUDE.md` |
| `glossary.md` | `templates/glossary.md` |
| `docs/adr/README.md` | `templates/docs/adr/README.md` |
| `docs/tracker/README.md` | `templates/docs/tracker/README.md` |
| `docs/tracker/<division>/.gitkeep` | empty, one per division |
| `skills/README.md` | `templates/skills/README.md` |
| `architecture/.gitkeep` | empty |
| `contract/.gitkeep` | empty |
| `apps/.gitkeep` | empty |
| `.gitignore` | `templates/.gitignore` |
| `.claude/skills` | symlink to `../skills` |
| `.agents/skills` | symlink to `../skills` |

Create only these paths. `docs/prd.md`, `docs/fsd.md`, `architecture/*.md` and `contract/*` belong to their owner skills: each downstream skill checks that its upstream artifact exists, so an absent file is the honest signal that the step has not run.

The three shared templates (`glossary.md`, `docs/adr/README.md`, `docs/tracker/README.md`) are the single source of truth for those formats inside the project. Every other skill reads them from the project.

## Process

### 1. Explore

The target is the current working directory unless the user names another. For every path in the skeleton except the division `.gitkeep` files, record one state: absent, present, or (for the symlinks) a real directory or a symlink to another target. Divisions are chosen in step 2, so list the folders already under `docs/tracker/` instead. Also note whether the target is a git repo; report it, change nothing.

Done when every skeleton path except the division `.gitkeep` files has a state, and the existing `docs/tracker/` folders are listed.

### 2. Ask

In Indonesian, one question at a time:

1. Project name. Recommend the folder name.
2. Project description, 1-2 sentences. An open question with no recommended answer: only the user knows the project.
3. Divisions. Recommend the folders already under `docs/tracker/` if there are any, otherwise the default `dev`, `qc`, `ui-ux`; the user may add more. Slugs are lowercase kebab-case.

### 3. Confirm

Record the state of each chosen division's `docs/tracker/<division>/.gitkeep`. Show the user three lists: paths to create, paths already present (kept as they are), and conflicts. Wait for an explicit yes.

### 4. Write

- Write only to absent paths. Existing files stay byte-for-byte as they are.
- Copy each template, then replace the setup tokens:
  - `{{PROJECT_NAME}}`: the project name.
  - `{{PROJECT_DESCRIPTION}}`: the description.
  - `{{DIVISIONS}}`: one bullet per division, e.g. `` - `dev` ``.
- Keep every other `{{...}}`. Those are authoring placeholders inside the shared templates, filled later by the skill that writes each artifact.
- Symlinks: `mkdir -p .claude .agents`, then `ln -s ../skills .claude/skills` and `ln -s ../skills .agents/skills`.
- Existing `AGENTS.md` or `CLAUDE.md`: list the template sections it lacks and ask whether to add them.
- Existing `.gitignore`: list the template lines it lacks and ask whether to append them. `apps/*` and `!apps/.gitkeep` matter most: each app under `apps/` has its own repo.
- A conflict (a real `skills` directory under `.claude/` or `.agents/`, or a symlink pointing elsewhere): leave it, report it, ask the user how to resolve it.

### 5. Verify

- `readlink .claude/skills .agents/skills` both print `../skills`.
- `grep -rnE '\{\{[A-Z_]+\}\}' AGENTS.md glossary.md docs/` prints nothing.
- `grep -xF 'apps/*' .gitignore` and `grep -xF '!apps/.gitkeep' .gitignore` each print one line.

Done when all three checks pass. Report what was created, kept and skipped, and name the next step: `project-grilling`.
