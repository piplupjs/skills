---
title: Read the Stack Before Picking Anything
impact: CRITICAL
impactDescription: sourced components install and theme cleanly instead of fighting the project
tags: context, tailwind, shadcn, tokens
---

## Read the Stack Before Picking Anything

**Impact: CRITICAL (sourced components install and theme cleanly)**

Every source here assumes React and Tailwind, and most ship as shadcn registry items. Before choosing one, check:

| Check | Where | Decides |
|-------|-------|---------|
| Tailwind version | `package.json`, `tailwind.config.*` or `@theme` in CSS | v3 vs v4 snippet variant |
| shadcn set up | `components.json` | CLI install vs manual copy, target folder |
| Existing tokens | `globals.css` CSS variables, `@theme`, config `theme.extend` | Colors, radius, fonts to map onto |
| Installed primitives | `components/ui/` | Reuse instead of adding a second button |
| Motion library | `motion` / `framer-motion`, GSAP | Whether effects add a dependency |
| Dark mode | `.dark` class or media query | Whether both themes must be checked |

If the project is not React + Tailwind, use the sources only as visual references and rebuild in the project's own stack.

**Incorrect (installs before looking; adds a second button and hard-coded palette):**

```bash
npx shadcn@latest init   # project already has components.json
```

**Correct (reads first, then adds only what's missing):**

```bash
cat components.json && ls src/components/ui
npx shadcn@latest add tabs   # only the primitive that isn't there yet
```

Reference: [shadcn/ui CLI](https://ui.shadcn.com/docs/cli)
