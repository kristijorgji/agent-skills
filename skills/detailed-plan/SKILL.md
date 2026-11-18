---
name: detailed-plan
description: >-
  Produce a detailed, ordered implementation plan a smaller model can follow.
  Use when the user explicitly invokes /detailed-plan or pastes numbered topics
  to plan.
disable-model-invocation: true
license: MIT
metadata:
  author: kristijorgji
  version: "1.0.0"
---

# Detailed Plan

Explicit-only. Do **not** load or follow this skill from ambient chat. Run it only when the user
invokes `/detailed-plan` or pastes numbered topics to plan.

## Standing rules

Use this wording as-is:

- Work on a new worktree only if the user asks for a worktree. If they do not, or you are confused
  about where to work, you must ask to confirm where it will work.
- If you have doubts about some topic you must ask me while you provide also your recommendation and
  reason why (after you do a proper research).
- You must never consider the plan ready if you are not 100% sure confident.
- You can use browser tools if needed and check production with readonly credentials when the
  project documents how (see Optional project config).
- The plan must be very detailed so smaller model can follow with ease.
- The plan todos order must match my ordering.
- If you fix a bug you must update existing test (preferred) or create a new one to assert this
  behavior (bug) won't repeat anymore.
- While planning you must reuse existing functions, code whenever possible instead of creating
  duplications.

## Optional project config

If the project has agent-local config (commonly `.agents/config.local.json`, often gitignored),
read it for paths and readonly production access the user already set up.

1. Prefer an example file in the repo (e.g. `.agents/config.local.json.example`) over inventing
   keys. If required local config is missing, tell the user what to create — do not invent secrets.
2. Never commit machine-specific paths or secrets.
3. Fail fast if a path or script you need does not exist.
4. Never print passwords, dump PII, or paste secrets into the plan or chat.

If the project has no such config, plan from the codebase and public docs only.

## Workflow

### Planning (read-only)

1. If the agent supports plan mode and you are not already in it, switch to plan mode.
2. Stay in the current checkout. Do **not** create a worktree or edit files yet.
3. Load optional project config when present and needed. Fail fast on missing `CHANGE_ME` values
   you actually need.
4. Research each numbered topic in the user's order: code first, then browser / readonly prod DB /
   logs when the topic needs that evidence and the project documents how.
5. If you have doubts after research, ask with a recommendation and reason. Do not guess.
6. Do not finalize the plan until you are 100% confident on every topic.
7. Produce the plan:
   - **Cursor (or tools with `CreatePlan`):** call `CreatePlan`.
   - **Otherwise:** write an equivalent detailed plan the user can approve before implementation.
   Todo order **must** match the user's topic numbering (`1`, `2a`, `2b`, `2c`, `3`, …). Each
   lettered sub-item is its own todo. Do not reorder. If a later topic is a hard prerequisite for
   an earlier one, **ask** instead of silently reordering.

### After the user confirms the plan

Do **not** create a worktree unless the user asked for one.

- **User asked for a worktree:** use the project's documented worktree workflow if one exists;
  otherwise create an ordinary git worktree on a new branch from the agreed base and implement
  there.
- **User did not ask, or you are unsure:** ask where to work (current checkout vs new worktree).
  Include a recommendation and reason. Wait for confirmation before creating a worktree or editing.

## Plan quality

See [references/plan-quality.md](references/plan-quality.md). Summary:

- Name files, functions, and existing patterns to **reuse** (do not plan duplicate helpers)
- State the chosen approach (not "investigate later")
- Bug fixes: name the existing test to extend (preferred) or the new test to add
- Include verification (UI checks, tests, or other checks this repo expects)
- Cite production URLs or paths from the user's topics when relevant

## Production access (when configured)

Only when the project documents readonly production access and the topic needs it.

**Allowed during planning:** browser on documented prod URLs, readonly DB (`SELECT` only), log
tails via the project's documented SSH or log paths.

**Not allowed from this skill:** writes to prod DB, remote edits, service restarts, deploys, or
ad-hoc laptop deploy fallbacks (rsync/scp, S3 sync, supervisor restarts) unless the user explicitly
invokes a separate deploy skill or instructs otherwise.

Never print credentials. Prefer sample rows, counts, and schema over dumping PII.
