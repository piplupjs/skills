---
title: Use One Base Component System
impact: HIGH
impactDescription: one consistent set of primitives instead of competing buttons and inputs
tags: sourcing, shadcn, alignui, primitives
---

## Use One Base Component System

**Impact: HIGH (one consistent set of primitives)**

Buttons, inputs, selects, dialogs, tables, and tabs come from exactly one system. Pick in this order:

1. **The one already installed.** Keep it, even if another looks nicer.
2. **[shadcn/ui](https://ui.shadcn.com/)** otherwise: open-source, copied into the repo, themed by CSS variables. The default.

[AlignUI Pro](https://pro.alignui.com) is a polished product kit, strong for dashboards, app shells, and settings. Use its screens as the design reference and build your own implementation with the base system's primitives; don't add it as a second system.

Every other source in this skill builds on top of the base system; none of them replaces it.

**Incorrect (two systems' buttons on one page):**

```tsx
import { Button } from "@/components/ui/button";       // shadcn
import { Button as AButton } from "@/components/align/button";   // second system
```

**Correct (one system, variants for differences):**

```tsx
import { Button } from "@/components/ui/button";

<Button>Save</Button>
<Button variant="outline">Cancel</Button>
```

Reference: [shadcn/ui](https://ui.shadcn.com/docs)
