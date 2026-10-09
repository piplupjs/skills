---
title: Bound Features by Backend Domain
impact: HIGH
impactDescription: one feature per backend module and API path
tags: features, boundaries, api
---

## Bound Features by Backend Domain

**Impact: HIGH (one feature per backend module and API path)**

Draw feature boundaries from the backend module and API path that serves them, not from a broad product label or a shared URL prefix. `/api/invoices` and `/api/payments` are two features even if both sit under a "Billing" menu.

**Incorrect (one folder per product label):**

```
features/billing/          # invoices, payments, refunds mixed together
```

**Correct (one folder per backend domain):**

```
features/invoices/
features/payments/
features/refunds/
```
