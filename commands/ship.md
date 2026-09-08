---
description: Final pre-ship gate -- diff review, full verification, and security check
agent: architect
---

Run the full ship gate before this change goes out: $ARGUMENTS

1. Get the current diff and summarize the scope of the change.
2. Run validator for build, types, lint, and tests.
3. Run auditor for a security/reliability pass on the diff.
4. Run reviewer for a final correctness and quality pass.
5. If any P0 or P1 issue is found, stop and send it to builder for a fix,
   then repeat validation.
6. Once everything is clean, produce a final summary: what changed, what was
   verified, what was found and fixed, and the current repository status.
