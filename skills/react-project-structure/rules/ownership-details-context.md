---
title: Load the Record Once in Details, Share It by Context
impact: MEDIUM
impactDescription: tabs never refetch the same record
tags: ownership, details, context
---

## Load the Record Once in Details, Share It by Context

**Impact: MEDIUM (tabs never refetch the same record)**

The `details/` area loads the record once and provides it through a context (`details/context/<entity>-detail.context.tsx`). Child tabs (`profile/`, `payments/`, …) read it from that context and never fetch the same record again. How the record is loaded (route loader, query hook, server component) is the framework's concern.

**Incorrect (each tab fetches the record):**

```tsx
export function InvoicesProfileView({ id }: { id: string }) {
  const { data: invoice } = useQuery(invoiceDetailQuery(id));
  // ...
}
```

**Correct (tab consumes the details context):**

```tsx
export function InvoicesProfileView() {
  const invoice = useInvoiceDetail();
  // ...
}
```
