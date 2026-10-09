---
name: tanstack-start-project-structure
description: Organizes a TanStack Start app's routing and wiring - thin file routes, detail shells with one route per tab, loaders that prefetch query options, route-wired loading and error views, and one home each for the router, start entry, config, and generated route tree. Use when adding or changing routes in TanStack Start or TanStack Router, or when the user says "add a route", "new page", "detail page with tabs", "loader", "pendingComponent", "errorComponent", or "routeTree.gen.ts".
when_to_use: |
  - Adding, moving, or renaming a route file under src/routes in a TanStack Start or TanStack Router app
  - Building a list, detail, or tabbed detail page and wiring its params, search schema, loader, and loading/error views
  - Editing the router module, src/start.ts, config/client.ts or config/server.ts, or regenerating routeTree.gen.ts
  - Reviewing a route file that renders markup, fetches in the view instead of the loader, or misses its error view
  - Do NOT use for: Next.js, React Router, or other frameworks; feature folder layout (react-project-structure); server function or middleware API details
license: MIT
metadata:
  author: piplupjs
  version: "1.0.0"
---

# TanStack Start Project Structure

The TanStack Start layer on top of `react-project-structure`: routes, loaders, and app wiring. Everything under `features/` follows `react-project-structure`. Not for Next.js, React Router, or other frameworks, feature folder layout, or server function and middleware API details.

## Workflow

1. **Route**: add the file at its URL in the tree; keep it to route options only.
2. **Load**: prefetch the feature's query options in the loader; wire the feature's loading and error views.
3. **Regenerate**: rebuild the route tree after changing the files.
4. **Review**: one pass over the quick reference; open a rule file when a check fails.

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Routes | CRITICAL | `routes-` |
| 2 | Data Loading | HIGH | `loader-` |
| 3 | App Wiring | MEDIUM | `app-` |

## Quick Reference

### 1. Routes (CRITICAL)

- `routes-file-tree`: Pathless layouts (`_app`), optional params (`{-$locale}`), a layout file beside its folder
- `routes-thin-file-route`: A route file holds only `createFileRoute` options and a feature view as `component`
- `routes-detail-shell`: `$id.tsx` loads the record and renders the shell; `$id/index.tsx` is the default tab; one route per tab
- `routes-search-schema-in-feature`: `validateSearch` imports its schema (and default filters) from the feature

### 2. Data Loading (HIGH)

- `loader-prefetch-only`: Loaders prefetch query options into the cache; views read the same options with `useQuery`
- `loader-pending-error`: Every route with a loader sets `pendingComponent` and `errorComponent` from the feature

### 3. App Wiring (MEDIUM)

- `app-router`: One module exports `getRouter()` with the route tree, router context, and defaults
- `app-start`: `src/start.ts` holds `createStart` and global middleware
- `app-config-split`: `config/client.ts` and `config/server.ts` are the public config API; shared helpers stay internal
- `app-route-tree-generated`: Regenerate `routeTree.gen.ts`; never edit it

## How to Use

Read individual rule files for the full rule and examples:

```
rules/routes-detail-shell.md
rules/loader-pending-error.md
```

Section metadata lives in `rules/_sections.md`; new rules start from `rules/_template.md`.
