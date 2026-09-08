---
description: Investigate a problem and produce an implementation plan with no code changes
agent: architect
---

Investigate the following without making any code changes: $ARGUMENTS

1. Send the problem to deep-thinker first. Do not let it propose an
   implementation — it should surface assumptions, constraints,
   alternatives, and failure modes.
2. Send the same problem to decomposer to sketch the shape of the work:
   tasks, dependencies, parallelizable pieces, and risk areas.
3. Synthesize both outputs yourself into a single implementation plan:
   recommended approach, why it beats the alternatives, open risks, and the
   ordered task breakdown.
4. Do not invoke builder, test-engineer, validator, reviewer, or auditor for
   this command — it is planning only.
