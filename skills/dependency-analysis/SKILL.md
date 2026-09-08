---
name: Dependency Analysis
description: Method for understanding what a change affects before making it -- callers, shared state, and version/dependency risk.
---

## Before changing shared code

- Find every caller/usage of what you're about to change, not just the
  ones you already know about — a broad search beats memory.
- Check for shared mutable state that a change in behavior could affect
  indirectly.
- If the signature or behavior of something widely used is changing,
  enumerate the call sites that need updating before starting, so the size
  of the change is known up front rather than discovered mid-way.

## Before adding a new dependency

- Check its transitive dependencies and known vulnerabilities, not just the
  package itself.
- Weigh its maintenance and security surface against the amount of code it
  actually saves you — a small amount of code you own outright is
  sometimes better than a dependency you don't control.
- Check it's actively maintained; an abandoned dependency is a future
  migration you're signing up for.

## Rule

"What does this touch?" is a question to answer before the change, not a
surprise to discover from a failing test after.
