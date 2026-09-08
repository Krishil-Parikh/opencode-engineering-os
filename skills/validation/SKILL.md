---
name: Validation
description: Defines what "done" means before something ships -- the exact set of checks to run and the report format to use.
---

## What "done" requires

1. The project builds.
2. The type checker passes.
3. The linter passes.
4. The full unit test suite passes.
5. Relevant integration tests pass.
6. The specific changed behavior has been exercised, not just inferred from
   1-5.
7. Plausible edge cases for the change have been checked.

## Report format

```
VALIDATION RESULT

Build:        PASS / FAIL
Types:        PASS / FAIL
Lint:         PASS / FAIL
Unit tests:   <passed>/<total>
Integration:  PASS / FAIL / N/A

Changed behavior:
  ✓ <thing that was verified working>

Potential concern:
  ⚠ <anything undertested or fragile, short of an outright failure>

Verdict: PASS / PASS WITH WARNING / FAIL
```

## Rules

- Report reproducible failures with the exact command and output — not a
  paraphrase of what went wrong.
- This is a mechanical check, not a design opinion. "It passes but I'd have
  built it differently" is a PASS here — that judgment belongs in
  [Code Review](../code-review/SKILL.md).
