---
title: Put What Sibling Areas Share at the Feature Root
impact: HIGH
impactDescription: shared feature code has one home
tags: features, reuse, lib
---

## Put What Sibling Areas Share at the Feature Root

**Impact: HIGH (shared feature code has one home)**

Helpers, components, and schemas used by several areas of the same feature go in the feature root (`features/<feature>/lib/`, `components/`, `schema/`), not in one area that the others then import from.

```
features/invoices/
  lib/invoice-status.ts          # used by list/, details/, profile/
  components/invoice-status-badge.tsx
  list/
  details/
```
