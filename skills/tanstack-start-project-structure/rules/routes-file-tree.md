---
title: Shape the File Route Tree with Layouts and Optional Params
impact: CRITICAL
impactDescription: URLs, layouts, and guards map one-to-one to files
tags: routes, file-based-routing, layouts
---

## Shape the File Route Tree with Layouts and Optional Params

**Impact: CRITICAL (URLs, layouts, and guards map one-to-one to files)**

- Pathless layouts (`_app`, `_dashboard`) wrap routes in a shell or guard without adding a URL segment.
- Optional params (`{-$locale}`) cover URLs with and without the segment from one tree.
- A layout is a file next to its folder (`_app.tsx` beside `_app/`); its children live inside the folder.
- Folder segments mirror the URL; one feature's routes sit under one segment.

```
src/routes/
  __root.tsx
  {-$locale}.tsx
  {-$locale}/
    _app.tsx                 # app shell, no URL segment
    _app/
      login.tsx
      _dashboard.tsx         # signed-in layout
      _dashboard/
        invoices/
          index.tsx          # /invoices
          create.tsx         # /invoices/create
          $id.tsx            # /invoices/:id shell
          $id/
            index.tsx        # default tab
            payments.tsx     # /invoices/:id/payments
```
