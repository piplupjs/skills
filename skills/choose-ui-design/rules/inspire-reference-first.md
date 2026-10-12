---
title: Find References Before Writing Markup
impact: HIGH
impactDescription: replaces the generic AI-default layout with proven patterns
tags: inspiration, references, patterns
---

## Find References Before Writing Markup

**Impact: HIGH (proven patterns instead of the generic default)**

Without references, every page drifts to the same centered hero, three-card row, and purple gradient. Before writing markup, find 2–3 real examples of the same screen and write down the pattern in a few lines:

- **Layout**: columns, what sits above the fold, where the primary action is
- **Hierarchy**: what is biggest, what is muted, how many type sizes
- **States**: empty, loading, error, success
- **The one detail** that makes it feel finished

Then build that pattern with the project's own components. Copy structure and decisions, never a brand's logo, illustration, copy, or exact look.

**Incorrect (no reference, generic default):**

```text
Settings page: centered card, all fields in one long column, Save at the bottom.
```

**Correct (pattern extracted from references):**

```text
Refs: 3 settings screens (Mobbin)
Pattern: left section nav; right column of grouped cards, each with title + description;
save per card, sticky only when dirty; destructive actions isolated in a red-bordered last card.
```
