---
title: Keep File Routes Thin
impact: CRITICAL
impactDescription: routes wire, features render
tags: routes, createFileRoute, features
---

## Keep File Routes Thin

**Impact: CRITICAL (routes wire, features render)**

A route file holds only `createFileRoute` options: `params`, `validateSearch`, `loader`, `pendingComponent`, `errorComponent`, and `component` set to a feature view. No markup, hooks, or business logic. Feature folders follow `react-project-structure`.

**Incorrect (page built inside the route file):**

```tsx
export const Route = createFileRoute('/_app/invoices/')({
  component: () => {
    const { data } = useQuery(invoicesListQueryOptions());
    return <table>{/* ... */}</table>;
  },
});
```

**Correct (route selects the feature view):**

```tsx
import { invoicesListSearchSchema } from '@/features/invoices/list/schema/invoices-list.schema';
import { InvoicesListView } from '@/features/invoices/list/views/invoices-list.view';
import { createFileRoute } from '@tanstack/react-router';

export const Route = createFileRoute('/_app/invoices/')({
  validateSearch: invoicesListSearchSchema,
  component: InvoicesListView,
});
```
