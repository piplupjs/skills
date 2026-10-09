---
title: Views Compose, Forms Own Fields
impact: MEDIUM
impactDescription: layout and form logic change independently
tags: ownership, views, forms
---

## Views Compose, Forms Own Fields

**Impact: MEDIUM (layout and form logic change independently)**

A view composes layout and picks the form; it holds no fields. A form owns its fields, validation, submission, and form-local controls. Reuse shared field definitions where the same fields occur in several workflows.

**Incorrect (view builds the form inline):**

```tsx
export function InvoicesCreateView() {
  const form = useForm({ /* fields, validation, submit */ });
  return <PageShell title="New invoice">{/* inputs... */}</PageShell>;
}
```

**Correct:**

```tsx
export function InvoicesCreateView() {
  return (
    <PageShell title="New invoice">
      <InvoicesCreateForm />
    </PageShell>
  );
}
```
