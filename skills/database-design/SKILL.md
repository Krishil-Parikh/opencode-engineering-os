---
name: Database Design
description: Checklist for schema and data-model decisions -- normalization tradeoffs, indexing, migrations, and consistency guarantees.
---

- **Normalization**: normalize to avoid update anomalies; denormalize
  deliberately, for a measured read-performance reason, not by default.
- **Indexing**: index for the queries you actually run, not the ones you
  imagine you might. Check the query plan, don't guess.
- **Migrations**: write them to be backward compatible with the
  currently-deployed code during rollout, and reversible where practical.
  A migration that requires simultaneous code deploy and schema change is a
  outage waiting to happen.
- **Consistency**: pick transaction boundaries that match the actual
  consistency requirement — not every write needs the same guarantee.
- **Concurrent writes**: work out what happens when two writers touch the
  same row at once, explicitly, rather than discovering it in production.

## Rule

A schema change is a contract change with every piece of code that reads or
writes that table — check for those callers before assuming a change is
safe (see [Dependency Analysis](../dependency-analysis/SKILL.md)).
