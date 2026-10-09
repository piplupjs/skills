---
title: Wire Loading and Error Views on the Route
impact: HIGH
impactDescription: loader failures and pending navigation reach the feature views
tags: loader, pendingComponent, errorComponent
---

## Wire Loading and Error Views on the Route

**Impact: HIGH (loader failures and pending navigation reach the feature views)**

Every route with a `loader` sets `pendingComponent` and `errorComponent` to the feature's `.loading.tsx` and `.error.tsx` views. When a loader throws, the route's `component` never renders, so a view cannot catch its own loader's failure; only the route's `errorComponent` sees it.

**Incorrect (error handling inside the view; loader errors skip it):**

```tsx
export const Route = createFileRoute('/_app/invoices/$id')({
  loader: ({ context, params }) =>
    context.queryClient.ensureQueryData(invoicesDetailQueryOptions(params.id)),
  component: InvoicesDetailView, // renders its own error state
});
```

**Correct:**

```tsx
export const Route = createFileRoute('/_app/invoices/$id')({
  loader: ({ context, params }) =>
    context.queryClient.ensureQueryData(invoicesDetailQueryOptions(params.id)),
  pendingComponent: InvoicesDetailLoading,
  errorComponent: InvoicesDetailError,
  component: InvoicesDetailView,
});
```
