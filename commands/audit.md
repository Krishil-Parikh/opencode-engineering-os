---
description: Run a read-only security, reliability, and architecture audit
agent: architect
---

Audit the codebase ($ARGUMENTS if a scope was given) with no modifications:

1. Run auditor for security and reliability findings (injection, auth,
   secrets, race conditions, resource exhaustion, and — where relevant —
   AI/ML-specific risks such as data leakage, evaluation contamination, and
   prompt injection).
2. Run reviewer for architecture and design-quality findings.
3. Run validator to report current build/type/lint/test health as a
   baseline.
4. Combine all three into one report ordered by severity (P0 first). Do not
   fix anything — this command only reports.
