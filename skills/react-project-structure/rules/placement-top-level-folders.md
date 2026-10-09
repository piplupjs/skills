---
title: Put Code in the Right Top-Level Folder
impact: CRITICAL
impactDescription: every file has one obvious home
tags: placement, folders, src
---

## Put Code in the Right Top-Level Folder

**Impact: CRITICAL (every file has one obvious home)**

The routing folder and the app entry are whatever the framework dictates (`app/`, `pages/`, `routes/`, `main.tsx`). Everything else under `src/` goes in one of these:

| Folder | Holds |
|---|---|
| `components/` | App-wide reusable UI: primitives, layout wrappers, generic blocks |
| `features/` | Feature slices: domain views, forms, services, schemas, feature-only components and hooks |
| `lib/` | Framework-agnostic utilities, API client, formatters, shared types |
| `hooks/` | App-wide reusable hooks |
| `providers/` | Third-party integrations and their providers (query client, i18n, analytics) |
| `styles/` | Global styles, design tokens, CSS entry |
| `config/` | Environment and runtime configuration |
| `generated/` | Codegen output: API clients, contracts, route trees |

Decide in this order: generated → `generated/`; provider integration → `providers/`; used by one feature → `features/<feature>/`; reusable UI → `components/`; reusable hook → `hooks/`; anything else shared → `lib/`.
