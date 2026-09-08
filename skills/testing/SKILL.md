---
name: Testing
description: Testing philosophy -- what to cover (unit, edge cases, failure paths, regression, integration) and how to tell whether a test actually proves anything.
---

## Process

```
What can go wrong?
        ↓
What behavior guarantees exist (explicit or implicit)?
        ↓
What tests prove those guarantees?
```

Read the implementation before designing tests. Testing from the ticket
alone tests the wrong thing.

## Coverage to aim for

- Unit tests for core logic, including the boring happy path.
- Edge cases: empty input, boundary values, unexpected types, concurrency.
- Failure tests: dependency errors, timeouts, malformed responses.
- Regression tests that encode any bug this change fixes.
- Integration tests at boundaries unit tests can't see (API, DB, external
  service).

## How to tell a test is real

- It fails when the behavior it claims to check is broken — actually try
  breaking the implementation and confirm the test catches it, for
  anything non-trivial.
- It tests behavior, not implementation details that are free to change.
- A guarantee you can't find a way to test should be noted explicitly, not
  quietly skipped.
