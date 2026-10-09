---
title: Detail Pages: Shell Route plus One Route per Tab
impact: CRITICAL
impactDescription: every tab has a URL, a crumb, and one shared record load
tags: routes, details, tabs
---

## Detail Pages: Shell Route plus One Route per Tab

**Impact: CRITICAL (every tab has a URL, a crumb, and one shared record load)**

- `$id.tsx` validates the param, loads the record, and renders the detail shell (title, actions, tab bar, `<Outlet />`) from `details/`.
- `$id/index.tsx` renders the default tab (`profile/`) at the record's own URL.
- Every other tab is its own route (`$id/payments.tsx`), rendering that tab's feature view.
- Tabs read the record from the details context; they do not load it again.

```tsx
// $id.tsx
export const Route = createFileRoute('/_app/invoices/$id')({
  params: z.object({ id: z.string() }),
  loader: ({ context, params }) =>
    context.queryClient.ensureQueryData(invoicesDetailQueryOptions(params.id)),
  pendingComponent: InvoicesDetailLoading,
  errorComponent: InvoicesDetailError,
  component: InvoicesDetailView,
});

// $id/index.tsx
export const Route = createFileRoute('/_app/invoices/$id/')({
  component: InvoicesProfileView,
});
```
