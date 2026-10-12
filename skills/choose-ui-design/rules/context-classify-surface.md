---
title: Classify the Surface Before Choosing Sources
impact: CRITICAL
impactDescription: marketing flair stays out of product screens and product screens stay usable
tags: context, marketing, dashboard, product
---

## Classify the Surface Before Choosing Sources

**Impact: CRITICAL (each surface gets the sources built for it)**

Marketing pages are seen once and must persuade; product screens are used daily and must be fast to scan. They need different sources.

| Surface | Examples | Reference | Build from | Effects |
|---------|----------|-----------|------------|---------|
| Marketing | Landing, pricing, changelog, waitlist | Kargul, bentogrids.com | shadcnblocks + base system | One signature effect, a background |
| Product | Dashboard, settings, tables, forms, onboarding | Mobbin flows, Kargul details | Base system primitives | Micro-interactions only |
| Hybrid | Auth pages, empty states, upgrade modals | Mobbin + Kargul | Base system, optional background | At most a subtle one |

**Incorrect (marketing effect on a product screen):**

```tsx
<SpotlightCard>          {/* Aceternity effect on every row */}
  <InvoiceRow invoice={invoice} />
</SpotlightCard>
```

**Correct (plain primitives in product UI):**

```tsx
<TableRow>
  <InvoiceRow invoice={invoice} />
</TableRow>
```
