---
name: Architecture
description: Checklist for architecture and design decisions -- component boundaries, interfaces, data flow, state management, scalability, failure handling, and observability.
---

Work through these before committing to a design, in roughly this order:

## Component boundaries

- What's the single responsibility of this component? If the answer has
  "and," it's probably two components.
- Where does this boundary match an existing seam in the codebase, and
  where does it cut across one?

## Interfaces

- What's the smallest interface that lets callers do what they need?
- Does this interface leak implementation details a caller shouldn't need
  to know?

## Data flow

- Where does data enter, and is it validated at that boundary or trusted
  downstream?
- Can you draw the flow in one pass without backtracking to explain a loop?

## State management

- What's the source of truth, and is there ever more than one?
- What happens to in-flight state if this process restarts?

## Scalability

- What's the actual expected load, and does this design's bottleneck show
  up before or after that number?
- Does this scale by adding resources, or does it need a redesign past a
  certain point? Is that point close enough to matter?

## Failure handling

- What's the failure mode for each external dependency (timeout, error,
  garbage response, hang)?
- Does a partial failure leave anything in an inconsistent state?

## Observability

- If this breaks in production, what signal tells you it broke, and how
  fast?
- Can you tell *why* it failed from the logs/metrics, or only *that* it
  did?
