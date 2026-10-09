---
title: Create the Router in One Module
impact: MEDIUM
impactDescription: router options and context have one home
tags: app, router, context
---

## Create the Router in One Module

**Impact: MEDIUM (router options and context have one home)**

One module (`src/router.tsx` by default, or a custom path such as `src/app/router.tsx` set in the `tanstackStart({ router: { entry } })` plugin option) exports `getRouter()`. It creates the router with the generated `routeTree`, the router context (such as `queryClient`), and router-wide defaults, and registers the router type. The root route declares that context with `createRootRouteWithContext`.

```tsx
export function getRouter() {
  const queryClient = new QueryClient();
  const router = createRouter({ routeTree, context: { queryClient }, defaultPreload: 'intent' });
  setupRouterSsrQueryIntegration({ router, queryClient });
  return router;
}

declare module '@tanstack/react-router' {
  interface Register {
    router: ReturnType<typeof getRouter>;
  }
}
```
