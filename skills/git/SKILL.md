---
name: Git
description: Conventions for commits, branches, and history -- atomic commits, clear messages, and when to open a PR vs. commit directly.
---

## Commits

- One logical change per commit. If the message needs "and" to describe it,
  it's probably two commits.
- Message: imperative mood, what changed and why, not a restatement of the
  diff. "Fix stale cache after invalidate()" beats "update cache.ts".
- Don't mix a refactor and a behavior change in the same commit — see the
  [Refactoring](../refactoring/SKILL.md) skill.

## Branches

- Name branches for what they do, not who's doing it or when.
- Never force-push a shared branch other people are actively working from.
  A force-push to your own not-yet-shared branch is fine.

## Pull requests

- The description states what changed, why, and how it was verified — link
  to (or restate) the validator result, don't just say "tested."
- Keep PRs reviewable in size. If decomposer's task breakdown produced
  independent pieces, consider shipping them as separate PRs.

## Rebase vs. merge

- Rebase your own feature branch onto the latest target branch before
  opening or updating a PR, to keep history readable.
- Don't rewrite history that's already been pushed and reviewed by someone
  else without asking first.
