---
title: Name Files in kebab-case
impact: MEDIUM
impactDescription: consistent, case-safe file names
tags: naming, files, hooks
---

## Name Files in kebab-case

**Impact: MEDIUM (consistent, case-safe file names)**

All files and folders are kebab-case. Hooks are `use-<name>.ts`; components keep PascalCase only as their export names.

**Incorrect:**

```
components/StatusBadge.tsx
hooks/useCountdown.ts
```

**Correct:**

```
components/status-badge.tsx
hooks/use-countdown.ts
```
