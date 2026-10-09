---
title: Import Search Schemas from the Feature
impact: CRITICAL
impactDescription: the list and its URL state change together
tags: routes, validateSearch, search-params
---

## Import Search Schemas from the Feature

**Impact: CRITICAL (the list and its URL state change together)**

`validateSearch` uses a schema that lives in the feature (`features/<feature>/list/schema/<feature>-list.schema.ts`), next to the view that reads it. Default filters belong in that schema, so the URL is the single source of list state.

**Incorrect (schema defined in the route file):**

```tsx
export const Route = createFileRoute('/_app/invoices/')({
  validateSearch: z.object({ page: z.number().default(1), status: z.string().optional() }),
  component: InvoicesListView,
});
```

**Correct:**

```tsx
export const Route = createFileRoute('/_app/invoices/')({
  validateSearch: invoicesListSearchSchema,
  component: InvoicesListView,
});
```
