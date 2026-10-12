---
title: Rewrite Sourced Styles to Project Tokens
impact: MEDIUM
impactDescription: pieces from five sources look like one product and follow dark mode
tags: fit, tokens, theming, tailwind
---

## Rewrite Sourced Styles to Project Tokens

**Impact: MEDIUM (five sources look like one product)**

Every source ships its own palette, radius, shadows, and fonts. After pasting, replace them with the project's tokens so the page reads as one product and switches theme correctly.

- Hard-coded colors (`bg-neutral-950`, `text-[#a3a3a3]`, `from-purple-500`) → semantic tokens (`bg-background`, `text-muted-foreground`, `from-primary`)
- Radius and shadow → the project's scale
- Fonts → the project's font variables; don't import the demo's font
- Spacing → the page's existing section rhythm

**Incorrect (demo palette kept):**

```tsx
<div className="rounded-3xl border border-neutral-800 bg-neutral-950 text-neutral-400">
```

**Correct (project tokens):**

```tsx
<div className="rounded-xl border bg-card text-muted-foreground">
```

Reference: [shadcn/ui theming](https://ui.shadcn.com/docs/theming)
