---
title: Mark the File Role with a Suffix
impact: MEDIUM
impactDescription: what a file is shows in its name
tags: naming, suffixes, files
---

## Mark the File Role with a Suffix

**Impact: MEDIUM (what a file is shows in its name)**

| Suffix | File | Folder |
|---|---|---|
| `.view.tsx` | Page-level view | `views/` |
| `.loading.tsx` | Loading view for a page | `views/` |
| `.error.tsx` | Error/retry view for a page | `views/` |
| `.form.tsx` | Form with its fields and submit | `components/` |
| `.dialog.tsx` | Dialog | `components/` |
| `.columns.tsx` | Table column definitions | `config/` |
| `.schema.ts` | Validation or URL search schema | `schema/` |
| `.service.ts` | Data access for one area | `services/` |
| `.context.tsx` | React context and its hook | `context/` |

Only `.view`, `.loading`, and `.error` files go in `views/`; menus, action bars, and items are components. Feature `.loading` and `.error` views are ordinary components that any route can render; they are not framework route conventions.
