---
name: Problem Solving
description: Structured method for approaching an ambiguous or complex problem before jumping to implementation -- define the problem, surface constraints and unknowns, generate real alternatives, and state a confidence level before committing.
---

## When to use this

Before implementing anything non-obvious: a feature with more than one
reasonable design, a bug whose cause isn't clear yet, or any request where
the first idea that comes to mind might not be the right one.

## Steps

1. **Define the problem** in one or two sentences. If you can't, that's the
   real problem — go find out what's actually being asked before doing
   anything else.
2. **Identify constraints** — what's genuinely fixed (compatibility,
   latency, data shape, team conventions) versus what only feels fixed.
3. **Identify unknowns** — what would you need to know to be confident? Can
   you find it out cheaply (read the code, check the docs) before guessing?
4. **Generate alternatives** — at least two real options, not a straw man
   next to your favorite.
5. **Determine the evidence required** to pick between them — a benchmark, a
   quick prototype, a look at existing usage patterns.
6. **Select an approach** and say why, specifically — not "this seems
   better" but "this handles X, which the alternative doesn't, and X matters
   because Y."
7. **State your confidence** and the one thing that would change your mind.

## Anti-pattern

Jumping to "here's the code" on step 1. If the first thing you produce is a
diff, the problem wasn't explored — it was assumed.
