---
description: Design, implement, test, and verify a change end to end
agent: architect
---

Run the full build pipeline for: $ARGUMENTS

1. Decompose the request with decomposer into ordered, dependency-aware
   tasks, with high-risk components flagged.
2. If the problem is ambiguous, involves a real tradeoff, or touches
   architecture, consult deep-thinker before committing to an approach.
3. Hand the resulting plan to builder for implementation. Builder must make
   minimal, behavior-preserving changes unless the request explicitly calls
   for a redesign.
4. builder delegates to test-engineer for unit, integration, and edge-case
   tests covering the new behavior.
5. Run validator to confirm the build, type checks, lint, and tests all
   pass.
6. Run reviewer and auditor independently for a quality and
   security/reliability pass.
7. Send any P0/P1 findings back to builder for fixes, then re-run validator.
8. Only report completion once validator passes and reviewer/auditor have no
   unresolved P0/P1 findings. Summarize what changed, what was verified, and
   any accepted risks.
