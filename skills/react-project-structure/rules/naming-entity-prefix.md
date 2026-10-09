---
title: Use One Entity Prefix per Feature
impact: MEDIUM
impactDescription: one search finds every page file of a feature
tags: naming, prefix, consistency
---

## Use One Entity Prefix per Feature

**Impact: MEDIUM (one search finds every page file of a feature)**

Every role-suffixed file in a feature (`.view`, `.loading`, `.error`, `.form`, `.dialog`, `.columns`, `.schema`, `.service`, `.context`) starts with the same entity prefix: the backend resource name (`/api/invoices` → `invoices-`), which is usually also the URL segment. Export names follow it. Do not mix singular and plural.

Plain components and `lib/` helpers are named for the concept they describe, which is often a single record (`lib/invoice-status.ts`, `components/invoice-status-badge.tsx`).

When the URL segment differs from the resource (a `/roles-and-permissions` page over `/api/roles`), use the resource: `roles-create.form.tsx`, not `roles-and-permissions-create.form.tsx`.

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
