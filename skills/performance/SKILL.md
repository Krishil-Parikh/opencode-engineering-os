---
name: Performance
description: Checklist for thinking through performance -- time, space, I/O, network, database, concurrency, caching, memory, and scaling -- before or after implementation.
---

Work through the dimensions that are actually relevant to the change —
not all of these apply every time.

- **Time**: what's the complexity class, and does it matter at your actual
  N (not a hypothetical one)?
- **Space**: what's held in memory at once, and does it grow with input
  size?
- **I/O**: how many round trips, and can any be batched or parallelized?
- **Network**: payload size, chattiness, and what happens under latency or
  packet loss.
- **Database**: are queries hitting an index, and do they scale with table
  size or row count returned?
- **Concurrency**: does this hold up under simultaneous access, or does it
  assume it's the only caller?
- **Caching**: is there a cache, and what invalidates it — could that
  invalidation be wrong or late?
- **Memory**: any unbounded growth (queues, caches, buffers) with no cap?
- **Scaling**: does this get better by adding resources, or does it hit a
  wall that needs a redesign — and how far off is that wall?

## Rule

Measure before optimizing. A guess about what's slow is often wrong, and
"optimizing" the wrong thing adds complexity for no benefit.
