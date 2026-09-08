---
name: Documentation
description: What to document and where -- code comments vs. README vs. AGENTS.md vs. ADRs -- and how to keep docs from rotting.
---

## Where things go

- **Code comments**: explain *why*, not *what* — the code already shows
  what it does. Comment the non-obvious reason a decision was made.
- **README**: setup, usage, and how to run/test the project. What a new
  contributor needs on day one.
- **AGENTS.md**: durable engineering conventions and standing rules that
  should apply to every session, not just this one change.
- **Architecture Decision Records (ADRs)**: decisions with real tradeoffs
  worth remembering later — what was chosen, what was rejected, and why.
  Write these when the "why not X" question is likely to come up again.

## Keeping docs from rotting

- Update documentation in the same diff as the change it describes, not as
  a follow-up that quietly never happens.
- If a doc and the code disagree, that's a bug — fix whichever one is
  wrong, don't leave the contradiction for the next reader to puzzle out.
- Prefer docs that are hard to go stale (generated references, doc comments
  next to the code) over ones that duplicate information that will drift.
