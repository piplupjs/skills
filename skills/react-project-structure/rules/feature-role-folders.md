---
title: Split an Area into Role Folders
impact: HIGH
impactDescription: the role of a file is visible from its folder
tags: features, folders, roles
---

## Split an Area into Role Folders

**Impact: HIGH (the role of a file is visible from its folder)**

Inside a page area, put each file in the folder for its role:

| Folder | Holds |
|---|---|
| `views/` | Page-level views and their loading/error views |
| `components/` | Pieces the views render: forms, dialogs, menus, actions, items |
| `services/` | Data access: API calls, query and mutation definitions |
| `schema/` | Validation and URL search schemas |
| `config/` | Static configuration such as table columns |
| `context/` | React context for data shared down the area |
| `lib/` | Pure helpers for the area |
| `hooks/` | Hooks used only by the area |

```
features/invoices/list/
  config/invoices-list.columns.tsx
  schema/invoices-list.schema.ts
  services/invoices-list.service.ts
  views/invoices-list.view.tsx
```
