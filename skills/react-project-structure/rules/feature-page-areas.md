---
title: Group a Feature by Page or Workflow
impact: HIGH
impactDescription: each page finds its files in one folder
tags: features, pages, workflows
---

## Group a Feature by Page or Workflow

**Impact: HIGH (each page finds its files in one folder)**

Inside a feature, group files by the page or workflow they serve:

| Area | Owns |
|---|---|
| `list/` | List view, column config, URL search schema, list queries |
| `details/` | The shared record load, context, title, actions, tab navigation, loading/error views |
| `profile/` | The default detail tab: its layout, form, validation, update |
| `create/`, `invite/`, `accept/`, … | Each workflow's own views, components, schemas, operations |
| One folder per extra tab | `members/`, `audit-logs/`, … with their own views and services |

```
features/invoices/
  list/
  details/
  profile/
  create/
  payments/        # a tab on the invoice detail page
```
