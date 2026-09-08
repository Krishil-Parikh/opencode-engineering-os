---
name: Incident Debugging
description: Response method for a live production incident -- stabilize first, understand second, and capture a postmortem once things are calm.
---

This is different from ordinary debugging: the priority order inverts.
Stopping the bleeding matters more than understanding it, at first.

## Steps

1. **Assess blast radius.** Who and what is actually affected, right now?
2. **Stabilize before you root-cause.** Rollback, feature-flag, rate-limit,
   or fail over — whatever gets impact down fastest, even if you don't yet
   know why it broke.
3. **Capture evidence while it's fresh**: logs, metrics, recent deploys or
   config changes, anything that might not be there in an hour.
4. **Identify the proximate trigger** — the thing that changed right before
   this started — even if it's not the full root cause. That's usually
   enough to decide on a mitigation.
5. **Communicate status at a fixed cadence** rather than going quiet while
   you dig.
6. Once stable, switch to the [Debugging](../debugging/SKILL.md) skill for
   the actual root cause.
7. **Write a blameless postmortem**: timeline, impact, root cause,
   contributing factors, and concrete follow-ups with owners and dates —
   not "we'll be more careful."

## Rule

Don't let curiosity about the root cause delay mitigation. You can
understand a fire after it's out.
