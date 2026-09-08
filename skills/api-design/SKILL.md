---
name: API Design
description: Checklist for designing APIs -- naming, versioning, error shapes, pagination, idempotency, and backwards compatibility.
---

- **Naming**: consistent verbs and nouns across endpoints; a new consumer
  should be able to guess the shape of an endpoint they haven't seen yet.
- **Versioning**: decide up front how a breaking change will be introduced
  (URL version, header, field deprecation window) rather than improvising
  when the first one is needed.
- **Error shapes**: one consistent error format across the whole API, with
  enough detail for a caller to act on it and not so much that it leaks
  internals.
- **Pagination**: cursor-based over offset-based for anything that can grow
  or mutate while being paged through.
- **Idempotency**: for anything that creates or mutates state, define what
  happens on a retried request — is it safe to call twice?
- **Backwards compatibility**: adding an optional field is usually safe;
  renaming, removing, or changing the type of an existing one usually isn't
  — treat it as a breaking change and version accordingly.

## Rule

Design the API from the caller's perspective first (what do they need to
express?), then check it against what the server can efficiently support —
not the other way around.
