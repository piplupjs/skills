---
name: react-project-structure
description: Organizes React app source into shared folders, backend-aligned feature slices, page areas, and role-suffixed files, independent of the framework or router. Use when creating files, folders, pages, or features in a React project, or when the user says "where should this go", "folder structure", "project structure", "organize features", "feature folders", or "this file is in the wrong place".
when_to_use: |
  - Creating a new file, folder, page, or feature in a React app (Next.js, React Router, TanStack Start, Vite SPA)
  - Deciding whether code is shared (components, lib, hooks) or owned by one feature
  - User asks "where should this go", about folder or project structure, or to reorganize features
  - Reviewing a change that puts files in the wrong layer, mixes prefixes, or scaffolds empty folders
  - Do NOT use for: code style inside a file, framework routing APIs (use that framework's structure skill), non-React projects, or monorepo package layout
license: MIT
metadata:
  author: piplupjs
  version: "1.0.1"
---

# React Project Structure

Where code lives in a React app, whatever the framework. The framework decides the routing folder and app entry; everything else follows these rules. Not for in-file code style, framework routing APIs, non-React projects, or monorepo package layout.

## Workflow

1. **Place**: pick the top-level folder with `placement-top-level-folders`; keep route modules thin.
2. **Slice**: inside `features/`, find the backend domain, then the page area, then the role folder.
3. **Name**: kebab-case, entity prefix, role suffix.
4. **Review**: one pass over the quick reference; open a rule file when a check fails.

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Placement | CRITICAL | `placement-` |
| 2 | Features | HIGH | `feature-` |
| 3 | Naming | MEDIUM | `naming-` |
| 4 | Ownership | MEDIUM | `ownership-` |

## Quick Reference

### 1. Placement (CRITICAL)

- `placement-top-level-folders`: `components/`, `features/`, `lib/`, `hooks/`, `providers/`, `styles/`, `config/`, `generated/`; routing folder and entry are the framework's
- `placement-routes-thin`: A route module only turns the URL into props and renders a feature view
- `placement-shared-vs-feature`: Keep code in its feature until a second feature needs it; never import another feature's internals
- `placement-generated-readonly`: Never hand-edit `generated/`; change the source and regenerate

### 2. Features (HIGH)

- `feature-backend-domain`: One feature per backend module/API path, not per product label
- `feature-page-areas`: Group by page or workflow: `list/`, `details/`, `profile/`, `create/`, one folder per tab
- `feature-role-folders`: Inside an area: `views/`, `components/`, `services/`, `schema/`, `config/`, `context/`, `lib/`, `hooks/`
- `feature-real-dirs-only`: Create only folders with a real responsibility
- `feature-shared-at-root`: What sibling areas share goes in the feature root

### 3. Naming (MEDIUM)

- `naming-kebab-case`: kebab-case files and folders; hooks are `use-*.ts`
- `naming-role-suffixes`: `.view`, `.loading`, `.error`, `.form`, `.dialog`, `.columns`, `.schema`, `.service`, `.context`; only views in `views/`
- `naming-entity-prefix`: One entity prefix (the backend resource name) for every role-suffixed file in a feature

### 4. Ownership (MEDIUM)

- `ownership-view-vs-form`: Views compose layout and pick forms; forms own fields, validation, submit
- `ownership-details-context`: `details/` loads the record once and shares it by context; tabs never refetch

## How to Use

Read individual rule files for the full rule and examples:

```
rules/placement-top-level-folders.md
rules/feature-page-areas.md
```

Section metadata lives in `rules/_sections.md`; new rules start from `rules/_template.md`.
