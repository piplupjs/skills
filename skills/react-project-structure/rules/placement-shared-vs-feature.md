---
title: Keep Code in Its Feature Until a Second Feature Needs It
impact: CRITICAL
impactDescription: shared folders hold only genuinely shared code
tags: placement, features, reuse
---

## Keep Code in Its Feature Until a Second Feature Needs It

**Impact: CRITICAL (shared folders hold only genuinely shared code)**

Code used by one feature lives in that feature, even if it looks reusable. Move it to `components/`, `lib/`, or `hooks/` when a second feature needs it, not before. Never import one feature's internals from another feature; promote the piece instead.
