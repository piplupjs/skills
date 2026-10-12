---
title: Stay Inside the Motion Budget
impact: MEDIUM
impactDescription: motion that delights once instead of tiring, distracting, or excluding users
tags: fit, motion, accessibility, performance
---

## Stay Inside the Motion Budget

**Impact: MEDIUM (motion delights instead of tiring)**

- **One** signature effect per marketing page; small hover and entrance transitions elsewhere.
- **None** of the showcase effects in product screens; use 150–250 ms transitions on state changes only.
- Respect `prefers-reduced-motion`: render the final state without animating.
- Don't animate text people must read (prices, legal, form labels) letter by letter.
- Lazy-load heavy effects (WebGL, canvas) below the fold, and stop them when off-screen.

**Incorrect (animation ignores reduced-motion):**

```tsx
<motion.h1 initial={{ opacity: 0, y: 40 }} animate={{ opacity: 1, y: 0 }}>
```

**Correct (reduced-motion users get the final state):**

```tsx
const reduce = useReducedMotion();

<motion.h1
  initial={reduce ? false : { opacity: 0, y: 40 }}
  animate={{ opacity: 1, y: 0 }}
>
```

Reference: [Motion: useReducedMotion](https://motion.dev/docs/react-use-reduced-motion)
