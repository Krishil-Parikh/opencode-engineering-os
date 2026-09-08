---
name: Code Review
description: Methodology for reviewing a diff -- what to check, how to phrase findings, and the severity taxonomy to classify them with.
---

## What to check

- Correctness beyond what tests cover.
- Maintainability — naming, structure, whether the next person can follow
  it without you.
- Coupling and abstraction boundaries.
- Race conditions and shared-state bugs.
- Error handling: loud and specific, or silent and vague?
- API design and backwards compatibility.
- Unnecessary changes riding along with the real diff.
- Test quality, not test coverage percentage.

## Severity taxonomy

```
P0   — catastrophic: data loss, security hole, breaks prod
P1   — serious bug: wrong behavior in a real path
P2   — should fix: real but non-urgent problem
P3   — improvement: worth doing, not blocking
NIT  — optional / style
```

## Finding format

Every finding needs a file, a line, and a concrete scenario — not an
adjective:

```
P1
src/cache.ts:87
Race condition between invalidate() and refresh().
Scenario: T1 reads stale value in refresh(); T2 invalidates; T1 writes the
stale value back.
Suggested fix: version-stamp cache entries; reject writes older than the
current stamp.
```

"Could be cleaner" is not a finding. If you can't point at a line and
describe what actually goes wrong, hold off until you can.

## Note

This is a review of design and correctness, not of whether the build,
tests, and linter pass — that's a separate, mechanical check (see the
[Validation](../validation/SKILL.md) skill).
