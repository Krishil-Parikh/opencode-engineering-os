---
description: Run the full verification suite and report pass/fail with no fixes
agent: validator
subagent: false
---

Run the complete verification suite for $ARGUMENTS (or the whole project if
empty): build, type checking, linting, unit tests, and any relevant
integration tests. Report a structured PASS/FAIL result per check, list any
reproducible failures with enough detail to act on, and flag untested edge
cases. Do not modify any files.
