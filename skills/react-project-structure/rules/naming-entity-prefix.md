---
title: Use One Entity Prefix per Feature
impact: MEDIUM
impactDescription: one search finds every file of a feature
tags: naming, prefix, consistency
---

## Use One Entity Prefix per Feature

**Impact: MEDIUM (one search finds every file of a feature)**

Every file in a feature starts with the same entity prefix, matching the feature's URL segment (`/invoices` → `invoices-`), and export names follow it. Do not mix singular and plural.

**Incorrect (mixed prefixes and exports):**

```
create/schema/invoice-create.schema.ts
create/services/invoices-create.service.ts
profile/views/invoice-profile.view.tsx   // exports InvoicesProfileView
```

**Correct:**

```
create/schema/invoices-create.schema.ts
create/services/invoices-create.service.ts
profile/views/invoices-profile.view.tsx  // exports InvoicesProfileView
```
