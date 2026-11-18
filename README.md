# Agent Skills

Reusable [Agent Skills](https://agentskills.io) for Cursor, Claude Code, Codex, and other compatible agents.

Install from this public GitHub repo — no npm publish required.

## Skills

| Skill | Invoke | Description |
|-------|--------|-------------|
| [`detailed-plan`](skills/detailed-plan/) | `/detailed-plan` | Explicit-only detailed planning for numbered topics; ordered todos a smaller model can follow |

## Quick start

```bash
npx skills add kristijorgji/agent-skills
```

Install one skill (project-level — current repo only):

```bash
npx skills add kristijorgji/agent-skills --skill detailed-plan
```

Install one skill globally (all Cursor projects / user-level):

```bash
npx skills add kristijorgji/agent-skills --skill detailed-plan -g
```

Browse without installing:

```bash
npx skills add kristijorgji/agent-skills --list
```

### Update after skill changes

When this repo publishes a newer version of a skill you already installed, refetch it:

```bash
# global install
npx skills update detailed-plan -g

# project install (run from that project)
npx skills update detailed-plan -p
```

Update every skill installed via the skills CLI:

```bash
npx skills update -g   # all global
npx skills update -p   # all project-level in the current repo
```

### Cursor

Project-level skills load from `.agents/skills/` or `.cursor/skills/`. User-level (global `-g`) from `~/.agents/skills/` or `~/.cursor/skills/`.

After `npx skills add`, invoke with `/detailed-plan` or ask the agent to use the `detailed-plan` skill.

### Claude Code

Marketplace:

```text
/plugin marketplace add kristijorgji/agent-skills
/plugin install agent-skills@kristijorgji-agent-skills
```

Or clone and load locally:

```bash
git clone https://github.com/kristijorgji/agent-skills.git
claude --plugin-dir /path/to/agent-skills
```

### Codex

Codex CLI v0.122+:

```bash
codex plugin marketplace add kristijorgji/agent-skills
codex plugin add agent-skills@agent-skills
```

## Layout

```text
skills/<skill-name>/SKILL.md   # canonical skills (agentskills + npx skills)
.claude-plugin/                # Claude Code marketplace / plugin
.codex-plugin/                 # Codex plugin
.claude/commands/              # thin slash-command wrappers
```

Each skill is self-contained under `skills/<name>/` (including any `references/`) so single-skill installs stay complete.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
