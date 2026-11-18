# Plan quality checklist

Use while drafting the plan. The plan must be detailed enough that a smaller model can implement
without re-researching.

## Required content

- [ ] Each user topic (`1`, `2a`, `2b`, …) maps to its own todo in the **same order**
- [ ] Chosen approach is stated concretely (no "investigate later" placeholders)
- [ ] Files, functions, modules, or patterns to **reuse** are named
- [ ] New code is justified only when reuse is not practical
- [ ] Bug fixes name an existing test to extend (preferred) or a new test to add
- [ ] Verification steps match the repo (tests, lint, browser, typecheck, etc.)
- [ ] Risks, migrations, and backwards-compat notes are called out when relevant
- [ ] Secrets and PII are absent from the plan text

## Todo shape (suggested)

For each topic:

1. **Goal** — one sentence
2. **Approach** — what to change and why this path
3. **Touch points** — paths / symbols
4. **Reuse** — existing helpers or patterns
5. **Tests** — update vs add
6. **Verify** — commands or manual checks

## Ordering conflicts

If topic N hard-depends on a later topic M:

- Do **not** silently reorder
- Ask the user, with a recommendation and reason, before changing order or splitting work
