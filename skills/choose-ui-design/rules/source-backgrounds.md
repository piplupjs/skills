---
title: Use Grainy Gradient Backgrounds Sparingly and Legibly
impact: HIGH
impactDescription: depth behind heroes without hurting load time or contrast
tags: sourcing, grainient, backgrounds, gradients
---

## Use Grainy Gradient Backgrounds Sparingly and Legibly

**Impact: HIGH (depth without hurting load time or contrast)**

[Grainient](https://grainient.supply) supplies grainy gradient backgrounds. Use them behind a hero, a CTA band, or a feature card, never behind body text, tables, or forms.

1. Pick hues from the project's brand or accent tokens, not a random palette.
2. Export at the size it displays and as AVIF/WebP; serve it with the framework's image component or `image-set()`.
3. Put text on a solid or blurred surface, or add an overlay, until it meets WCAG AA contrast.
4. Check it in dark mode; provide a darker variant or overlay if it glares.

**Incorrect (full-size PNG, text straight on the gradient):**

```tsx
<section style={{ backgroundImage: "url(/grainient-4k.png)" }}>
  <p className="text-white/70">Long paragraph…</p>
</section>
```

**Correct (optimized image, overlay for contrast):**

```tsx
<section className="relative isolate overflow-hidden">
  <Image src={heroBg} alt="" fill priority className="-z-10 object-cover" />
  <div className="absolute inset-0 -z-10 bg-background/40" />
  <HeroContent />
</section>
```

Reference: [Grainient](https://grainient.supply)
