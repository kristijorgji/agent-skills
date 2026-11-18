# Contributing

## Skill format

Each skill is a directory:

```text
skills/my-skill/
├── SKILL.md              # required
├── references/           # optional, loaded on demand
├── scripts/              # optional
└── assets/               # optional
```

`SKILL.md` must:

- Start with YAML frontmatter containing `name` and `description`
- Use a `name` that matches the parent directory (lowercase, hyphens, max 64 chars)
- Stay concise; move long detail into `references/`

Validate locally:

```bash
npx skill-check check skills --no-security-scan
```

## Pull requests

- One skill or one focused change per PR when practical
- Update the README skills table when adding a skill
- Do not commit secrets, `.env`, or machine-local config
