---
title: Start Marketing Sections From a Block
impact: HIGH
impactDescription: tested section layouts instead of hand-rolled ones
tags: sourcing, shadcnblocks, marketing, sections
---

## Start Marketing Sections From a Block

**Impact: HIGH (tested section layouts instead of hand-rolled ones)**

For hero, logos, features, testimonials, pricing, FAQ, CTA, and footer sections, start from a [shadcnblocks](https://www.shadcnblocks.com/) block built on shadcn/ui. Browse the category, pick the variant closest to the reference pattern, and install it with the command shown on the block's page (most are shadcn registry items).

Then adapt:

1. Replace placeholder copy, images, and links with real content.
2. Map colors, radius, and fonts to tokens (`fit-theme-tokens`).
3. Delete parts the page doesn't need; don't keep a stat row with fake numbers.
4. Vary neighbouring sections so the page isn't the same card grid five times.

For Pro blocks, use the design as the reference and rebuild it with the base system's primitives. Blocks are for marketing surfaces; product screens use base primitives.

Reference: [shadcnblocks](https://www.shadcnblocks.com/)
