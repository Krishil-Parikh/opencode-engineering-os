---
description: Refactor code while preserving existing behavior
agent: architect
---

Refactor the following with behavior held constant unless explicitly told
otherwise: $ARGUMENTS

1. If the refactor is non-trivial, consult deep-thinker on the target design
   and tradeoffs before touching code.
2. Hand the plan to builder. Hard rule: behavior must remain equivalent
   unless this request explicitly asked for a behavior change.
3. Run validator to confirm nothing broke.
4. Run reviewer to confirm the refactor actually improved the code rather
   than just moving it around.
5. Fix any issues and re-validate before reporting done.
