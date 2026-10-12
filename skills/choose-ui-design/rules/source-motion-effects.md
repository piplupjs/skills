---
title: Add One Signature Effect, Never Build On Effects
impact: HIGH
impactDescription: one memorable moment instead of a page that feels like a demo reel
tags: sourcing, aceternity, react-bits, motion, animation
---

## Add One Signature Effect, Never Build On Effects

**Impact: HIGH (one memorable moment instead of a demo reel)**

Effect libraries supply a single standout moment on a marketing page, layered on the base system:

| Source | Strong for | Ships as |
|--------|-----------|----------|
| [Aceternity UI](https://ui.aceternity.com/) | Hero effects: spotlight, beams, 3D/tilt cards, lamp, background grids | Tailwind + Motion (framer-motion) |
| [React Bits](https://reactbits.dev/) | Animated text (split, blur, shiny), animated backgrounds, cursor and hover toys | JS/TS × CSS/Tailwind variants |

Choose by the reference pattern, not by what looks coolest in the demo. Check the dependency it adds (`motion`, `gsap`, `three`/`ogl`) against `context-detect-stack`; a 3D/WebGL background is a large cost for one hero.

**Incorrect (effects as the building material):**

```tsx
<BackgroundBeams />
<SplitText text="Ship faster" />
<SpotlightCard><Features /></SpotlightCard>
<ShinyText text="Pricing" />
```

**Correct (one effect, everything else plain):**

```tsx
<section className="relative">
  <Spotlight className="-top-40 left-0" />
  <HeroContent />
</section>
<Features />   {/* base-system cards */}
```

Reference: [Aceternity UI](https://ui.aceternity.com/components), [React Bits](https://reactbits.dev/)
