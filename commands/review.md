---
description: Get an independent multi-perspective review of the current changes
agent: architect
---

Review the current changes ($ARGUMENTS if a specific scope was given,
otherwise the full diff):

1. Run reviewer, test-engineer, and auditor independently and in parallel —
   each should form its judgment without seeing the others' output.
2. reviewer reports on correctness, maintainability, and design quality with
   P0-NIT severity labels and file:line references.
3. test-engineer reports on test coverage gaps against the behavior actually
   implemented.
4. auditor reports on security, reliability, and data-integrity risk.
5. Synthesize all three into one report grouped by severity, noting any
   point where the perspectives disagree.
