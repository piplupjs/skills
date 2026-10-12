---
name: choose-ui-design
description: Chooses where a UI's design comes from before building it — reference patterns from Mobbin and Kargul's swipe file, base components from shadcn/ui or AlignUI Pro, page sections from shadcnblocks, motion from Aceternity UI or React Bits, bento layouts from bentogrids.com, and backgrounds from grainient.supply — then adapts the pick to the project's tokens. Use when building or redesigning a page, landing page, dashboard, or screen, or when the user says "make it look good", "make it modern", "this looks generic", "design a hero", "add a bento grid", "nicer background", "which component library", or "find inspiration".
when_to_use: |
  - Building a new page, screen, section, or app shell where the look is not already fully specified
  - User asks for a better or more modern look: "make it pop", "this looks generic", "looks like AI made it", "polish the UI"
  - Choosing a component library, a hero/feature/pricing section, an animated effect, a bento grid, or a background
  - User asks for UI inspiration, references, or "how do other apps do this screen"
  - Do NOT use for: in-file code style, folder structure, data/state logic, an existing design system or Figma file that already decides the look, or non-web UIs
license: MIT
metadata:
  author: piplupjs
  version: "1.0.0"
---

# Choose UI Design

Pick each layer of a UI from the source that does it best, after looking at how real products solve the same screen. Not for code style, folder structure, data logic, projects whose design system or Figma file already decides the look, or non-web UIs.

## Workflow

1. **Context**: read the stack and tokens (`context-detect-stack`), then classify the surface: marketing or product (`context-classify-surface`).
2. **Reference**: find 2–3 real examples of the same screen or flow and write down the pattern, not the pixels (`inspire-*`).
3. **Source**: one base system, then one source per layer from the map below (`source-*`).
4. **Fit**: map everything to the project's tokens, stay in the motion budget (`fit-*`).
5. **Report**: tell the user which reference and source each layer came from and why.

## Source Map

| Need | Source | Not for |
|------|--------|---------|
| How real apps lay out a flow or screen | [Mobbin](https://mobbin.com) | Copying a brand's look |
| Product detail and craft (empty states, toasts, settings) | [Kargul swipe file](https://kargul.studio/swipe-file) | Whole-page layout |
| Base primitives (button, input, dialog, table) | [shadcn/ui](https://ui.shadcn.com/) | Marketing flourishes |
| Polished product screens to rebuild with your primitives | [AlignUI Pro](https://pro.alignui.com) | A second base system |
| Whole marketing sections (hero, pricing, FAQ, footer) | [shadcnblocks](https://www.shadcnblocks.com/) | Dense app screens |
| One signature effect (spotlight, beams, 3D card) | [Aceternity UI](https://ui.aceternity.com/) | Forms, tables, dashboards |
| Animated text, backgrounds, small interactive pieces | [React Bits](https://reactbits.dev/) | Anything users read repeatedly |
| Feature showcase of 4–7 items with unequal weight | [Bento Grids](https://bentogrids.com) | Uniform lists or data |
| Grainy gradient hero or section backgrounds | [Grainient](https://grainient.supply) | Behind body text or tables |

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Context | CRITICAL | `context-` |
| 2 | Inspiration | HIGH | `inspire-` |
| 3 | Sourcing | HIGH | `source-` |
| 4 | Fit | MEDIUM | `fit-` |

## Quick Reference

### 1. Context (CRITICAL)

- `context-detect-stack`: Read Tailwind version, `components.json`, existing tokens and installed components before picking anything
- `context-classify-surface`: Marketing pages get sections and effects; product screens get primitives and real-app patterns

### 2. Inspiration (HIGH)

- `inspire-reference-first`: Find 2–3 references for the same screen before writing markup; extract the pattern
- `inspire-mobbin-flows`: Use Mobbin for flows and screen layouts; ask for screenshots when it is login-gated
- `inspire-kargul-details`: Use Kargul's swipe file for the small product details that make UI feel finished

### 3. Sourcing (HIGH)

- `source-one-base-system`: One base system: the one installed, else shadcn/ui; Pro designs are rebuilt on it
- `source-blocks-for-sections`: Start marketing sections from a shadcnblocks block, then adapt
- `source-motion-effects`: Aceternity UI or React Bits for one signature effect, never as the base
- `source-bento-grids`: Bento only for unequal-weight showcases; take the layout from bentogrids.com
- `source-backgrounds`: Grainient backgrounds behind heroes and section breaks, exported small, with readable text

### 4. Fit (MEDIUM)

- `fit-theme-tokens`: Rewrite every copied color, radius, and font to the project's tokens
- `fit-motion-budget`: One signature effect per page, `prefers-reduced-motion` respected, none in dense UI

## How to Use

Read individual rule files for the full rule and examples:

```
rules/context-classify-surface.md
rules/source-motion-effects.md
```

Section metadata lives in `rules/_sections.md`; new rules start from `rules/_template.md`.
