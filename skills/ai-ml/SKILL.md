---
name: AI/ML
description: Checklist specific to AI/ML work -- evaluation methodology, data leakage, retrieval vs. generation separation, and prompt-injection surface area.
---

- **Train/test separation**: confirm there's no leakage between splits —
  including leakage through preprocessing fit on the full dataset, or near-
  duplicate records across splits.
- **Evaluation methodology**: check that the metric actually measures the
  claim being made, and that the eval set represents the real distribution
  of inputs, not just the convenient one.
- **Retrieval vs. generation**: evaluate retrieval quality and generation
  quality separately where possible — a good generation over bad retrieval
  can look fine end-to-end while hiding the actual failure point.
- **Prompt injection surface**: anywhere retrieved documents, user input, or
  tool output reaches the model, treat it as untrusted and consider whether
  it could redirect behavior.
- **Grounding**: for anything presented as fact, check whether it's
  actually grounded in retrieved/verified content or is unsupported model
  output.
- **Fallback behavior**: define what happens when the primary model or
  provider is unavailable, rate-limited, or degraded — silent failure to a
  worse model is still a behavior change worth knowing about.
- **Reproducibility**: version prompts, datasets, and eval configs alongside
  code, so a result can be reproduced or compared later.

## Rule

A benchmark number without the eval methodology behind it is a claim, not
evidence. Ask what the number would look like if the methodology were
wrong.
