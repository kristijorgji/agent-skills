# AGENTS.md

Guidance for AI coding agents working on **this repository** (`kristijorgji/agent-skills`).

Reusable assets for other projects are the folders under `skills/`, not this file.

## Rules

- Keep each skill self-contained under `skills/<name>/` with a `SKILL.md` whose `name` matches the directory.
- Put on-demand detail in `skills/<name>/references/` — do not rely on a shared repo-level `references/` tree (single-skill installs would miss it).
- Follow the [Agent Skills specification](https://agentskills.io/specification): YAML frontmatter with `name` + `description`; keep `SKILL.md` under ~500 lines.
- Prefer `disable-model-invocation: true` for explicit-only workflows.
- Do not invent project-specific secrets, deploy scripts, or prod write access inside generic skills.
- After adding or editing a skill, ensure CI validation would pass (`npx skill-check check skills --no-security-scan`).

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md`
2. Add a short row to the README skills table
3. Optionally add a thin wrapper under `.claude/commands/<skill-name>.md`
