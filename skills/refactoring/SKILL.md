---
name: Refactoring
description: Rules for refactoring safely -- behavior must stay equivalent unless explicitly asked to change, and how to prove it didn't.
---

## The hard rule

Behavior must remain equivalent unless the request explicitly asked for a
behavior change. A refactor that also quietly changes behavior is two
changes wearing one diff, and it makes both harder to review and to revert.

## Steps

1. If the code isn't already well-tested, characterize its current behavior
   with tests first — you need a way to know if you broke something.
2. Refactor in small, independently verifiable steps rather than one large
   rewrite.
3. Re-run validation after each step, not just at the end.
4. Keep refactors and feature changes in separate diffs. If you notice a
   feature is needed mid-refactor, finish the refactor, then do the feature
   as its own change.

## Signs a "refactor" isn't one

- The diff touches behavior a test doesn't cover, and no one checked
  whether that behavior changed.
- It's justified by "cleaner" or "more idiomatic" rather than a concrete
  problem (hard to test, hard to extend, hard to understand) the current
  structure causes.
