---
name: Security Audit
description: Attack-focused checklist for security and reliability review -- injection, auth, secrets, SSRF, race conditions, resource exhaustion, and AI/ML-specific risks.
---

Adopt an adversarial mindset: assume the implementation is wrong and look
for evidence, rather than assuming it's fine and looking for reasons to
approve it.

## Security

- Injection: SQL, command, template, and prompt injection.
- Auth bypass and broken access control.
- Secrets hardcoded, logged, or leaked in error output.
- Unsafe deserialization, SSRF, path traversal.
- Known-vulnerable dependencies.

## Reliability

- Missing retries/timeouts, or retries with no backoff.
- Partial-failure handling — what's left inconsistent if this crashes
  halfway through?
- Race conditions, deadlocks, resource exhaustion.

## Data

- Corruption paths and unsafe/irreversible migrations.
- Consistency assumed but not enforced.
- Duplicate writes from retried operations.
- Missing validation at trust boundaries.

## AI/ML-specific

- Train/test leakage and evaluation contamination.
- Whether the evaluation methodology actually measures the claim being
  made.
- Prompt injection via retrieved documents, user input, or tool output.
- Retrieval poisoning and embedding mismatch.
- Model or provider fallback behavior under degradation.

## Reporting

Use the same severity taxonomy and finding format as
[Code Review](../code-review/SKILL.md). A finding with no reproducible
scenario is a hunch — label it as one rather than dressing it up.
