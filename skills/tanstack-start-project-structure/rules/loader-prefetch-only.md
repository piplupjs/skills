---
title: Loaders Prefetch, Views Read the Same Query
impact: HIGH
impactDescription: one cache entry feeds the route and the view
tags: loader, tanstack-query, ensureQueryData
---

## Loaders Prefetch, Views Read the Same Query

**Impact: HIGH (one cache entry feeds the route and the view)**

A loader only prefetches into the query cache, using the feature's query options; it returns nothing the view depends on. The view reads the same query options with `useQuery` (or `useSuspenseQuery`), so refetches, invalidation, and the loader share one cache entry. Pass the query client through router context.

**Incorrect (view depends on loader data that never refreshes):**

```tsx
loader: async ({ params }) => fetchInvoice(params.id),
// view: const invoice = Route.useLoaderData();
```

**Correct:**

```tsx
loader: ({ context, params }) =>
  context.queryClient.ensureQueryData(invoicesDetailQueryOptions(params.id)),
// view: const { data: invoice } = useQuery(invoicesDetailQueryOptions(id));
```
