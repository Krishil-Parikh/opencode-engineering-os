---
name: Debugging
description: Evidence-driven method for root-causing a bug -- reproduce, isolate a minimal failing case, form and test hypotheses, and turn the fix into a regression test.
---

## The chain

```
Symptom
  ↓
Reproduction
  ↓
Minimal failing case
  ↓
Hypotheses
  ↓
Evidence
  ↓
Root cause
  ↓
Fix
  ↓
Regression test
```

Skipping a link in this chain is how "fixes" that don't fix anything happen.

## Rules

- Reproduce it first. A bug you can't reproduce is a bug you can't confirm
  you fixed.
- Shrink the reproduction to the smallest case that still fails — strip
  everything that isn't necessary to trigger it.
- Form an explicit hypothesis before changing code: "I believe X causes this
  because Y." Then find evidence for or against it — a log line, a debugger
  breakpoint, a print statement — before touching the fix.
- Never ship "I think changing X should fix it" without having watched it
  actually fix the reproduction.
- Once fixed, write a regression test that encodes the original bug. If it
  can't be expressed as a test, you probably don't understand the root
  cause yet.
