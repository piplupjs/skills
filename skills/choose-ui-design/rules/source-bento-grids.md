---
title: Use Bento Only for Unequal-Weight Showcases
impact: HIGH
impactDescription: bento communicates hierarchy instead of decorating a uniform list
tags: sourcing, bento, layout, grid
---

## Use Bento Only for Unequal-Weight Showcases

**Impact: HIGH (bento shows hierarchy, not decoration)**

A bento grid works when 4–7 items have different importance: the headline feature gets the big tile, supporting ones get small tiles. For items of equal weight, a plain grid or list is clearer.

Take the layout from [Bento Grids](https://bentogrids.com) (a curated gallery of real bento sections): pick one whose tile count and proportions match the content, then build it with CSS grid and the base system's card.

- Each tile shows something (a mini UI, chart, or visual), not just an icon and paragraph.
- Collapse to one column on mobile, biggest tile first.
- Keep gaps and radius consistent with the rest of the page.

**Incorrect (equal items forced into uneven tiles):**

```tsx
<div className="grid grid-cols-3 gap-4">
  <Card className="col-span-2">Fast</Card>
  <Card>Secure</Card>
  <Card>Reliable</Card>
  <Card className="col-span-2">Simple</Card>
</div>
```

**Correct (tile size follows importance):**

```tsx
<div className="grid gap-4 md:grid-cols-3 md:grid-rows-2">
  <Card className="md:col-span-2 md:row-span-2"><LiveDashboardPreview /></Card>
  <Card><IntegrationsLogos /></Card>
  <Card><UptimeSparkline /></Card>
</div>
```

Reference: [Bento Grids](https://bentogrids.com)
