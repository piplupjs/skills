---
title: Keep Route Modules Thin
impact: CRITICAL
impactDescription: routing stays swappable and pages stay findable in features
tags: placement, routes, pages
---

## Keep Route Modules Thin

**Impact: CRITICAL (routing stays swappable and pages stay findable in features)**

Whatever the router (file-based or config-based), a route module only turns the URL into props and renders a feature view. Params and search validation, data-loading hooks the framework requires, and loading/error wiring are fine; business logic, markup, and forms are not.

**Incorrect (page markup and logic in the route module):**

```tsx
// routes/invoices/index.tsx
export default function InvoicesPage() {
  const { data } = useQuery(invoicesQuery());
  return (
    <section>
      <h1>Invoices</h1>
      <table>{/* ... */}</table>
    </section>
  );
}
```

**Correct (route selects the feature view):**

```tsx
// routes/invoices/index.tsx
import { InvoicesListView } from '@/features/invoices/list/views/invoices-list.view';

export default InvoicesListView;
```
