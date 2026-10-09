---
title: Never Edit Generated Code
impact: CRITICAL
impactDescription: regeneration never wipes hand edits
tags: placement, generated, codegen
---

## Never Edit Generated Code

**Impact: CRITICAL (regeneration never wipes hand edits)**

Everything in `generated/` (API clients, contracts, route trees, any codegen output) is rewritten by its generator. Never edit it by hand; change the source (schema, backend contract, route files) and regenerate. Wrap generated bindings behind feature services instead of patching them.
