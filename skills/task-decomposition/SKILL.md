---
name: Task Decomposition
description: Break a goal into an ordered, dependency-aware set of tasks with parallelizable work and risk called out by blast radius rather than difficulty.
---

## Shape of the output

```
epics
 └── tasks
      └── subtasks
           └── atomic implementation units
```

Every task carries: what depends on it, what it depends on, its risk level,
and what "done" looks like.

## Steps

1. State the goal in one line.
2. List tasks in the order their dependencies require, not the order they
   occurred to you.
3. Mark dependencies explicitly: `A → B → C`, `A → D`, `B + D → E`.
4. Identify what can run in parallel — anything with no shared dependency.
5. Classify risk by **blast radius and reversibility**, not difficulty:
   - High risk: auth, concurrency, external APIs, migrations, anything
     touching money or irreversible state.
   - Low risk: UI, formatting, isolated utilities, anything easy to revert.
6. Write acceptance criteria per task (or per group) — concrete enough that
   someone else could verify it without asking you what you meant.

## Anti-pattern

A flat, unordered to-do list. If nothing in the list depends on anything
else, you haven't actually decomposed the problem — you've just listed
adjectives for the same blob of work.
