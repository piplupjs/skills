# skills

Agent Skills for [skills.sh](https://skills.sh) / `npx skills`-compatible
coding agents (Claude Code, Cursor, Codex, OpenCode, and 25+ others).

## Install

```bash
npx skills add piplupjs/skills --skill code-spacing
npx skills add piplupjs/skills --skill coding-principles
npx skills add piplupjs/skills --skill write-react-code
npx skills add piplupjs/skills --skill react-project-structure
npx skills add piplupjs/skills --skill tanstack-start-project-structure
npx skills add piplupjs/skills --skill choose-ui-design
npx skills add piplupjs/skills --skill claude-delegate-and-budget
```

Add `-g` to install globally instead of per-project, or `-a <agent>` to
target a specific agent (e.g. `-a claude-code`).

List everything in this repo first if you want to see what's available:

```bash
npx skills add piplupjs/skills --list
```

## Skills in this repo

### `code-spacing`

Teaches an AI coding agent good vertical-whitespace (blank line) conventions
when writing, refactoring, or reviewing code — for readability and developer
experience.

Core rule: a blank line marks a conceptual boundary, not a decoration. Covers:

- grouping logically related lines vs. separating distinct steps
- never padding the inside of a block
- collapsing runs of multiple blank lines to one
- spacing between functions, classes, and methods (with the Python 2-blank-line
  exception called out)
- import spacing, comment placement, and return/throw statements
- a language quick-reference table (Python, JS/TS, Java, Go, C/C++, Rust, SQL)
- deferring to an existing formatter (Prettier, Black, gofmt, rustfmt) when
  one is configured

See `skills/code-spacing/SKILL.md` for the index and `skills/code-spacing/rules/` for one file per rule.

### `coding-principles`

Applies core software-engineering principles (DRY, SOLID, YAGNI, KISS, and
related design heuristics) whenever writing, reviewing, refactoring, or
reasoning about code. Governs how code should be structured (not what it should
do), so it applies to any coding task regardless of language or framework.

Priority order when principles conflict: correctness > clarity/simplicity
(KISS, YAGNI) > non-repetition (DRY) > extensibility (SOLID, OCP). Includes a
concrete application workflow for writing new code and reviewing/refactoring
existing code, with guidance on surfacing tradeoffs explicitly rather than
picking silently when principles conflict.

See `skills/coding-principles/SKILL.md` for the index and `skills/coding-principles/rules/` for one file per rule.

### `write-react-code`

Writes React components and hooks in one fixed, scannable shape. Covers:

- body order (State → Compute → Services → Compute → Form → Callbacks → Table
  → Effects) with padded section headers
- stable (`useCallback`) callback refs when an effect reads the ref
- repeated markup represented as data and rendered with `map`

See `skills/write-react-code/SKILL.md` for the index and `skills/write-react-code/rules/` for one file per rule.

### `react-project-structure`

Organizes a React app's source, whatever the framework or router (Next.js,
React Router, TanStack Start, Vite SPA). Covers:

- top-level folders (`components/`, `features/`, `lib/`, `hooks/`,
  `providers/`, `styles/`, `config/`, `generated/`) and thin route modules
- feature slices bounded by backend domain, grouped by page area (`list/`,
  `details/`, `profile/`, `create/`, one folder per tab), split by role folder
- kebab-case names, one entity prefix per feature, role suffixes (`.view`,
  `.form`, `.dialog`, `.schema`, `.service`, …)
- views vs forms, and loading a detail record once and sharing it by context

See `skills/react-project-structure/SKILL.md` for the index and `skills/react-project-structure/rules/` for one file per rule.

### `tanstack-start-project-structure`

The TanStack Start layer on top of `react-project-structure`. Covers:

- the file route tree: pathless layouts, optional params, thin file routes
- detail pages as a shell route plus one route per tab
- loaders that prefetch query options, with loading and error views wired on
  the route
- one home each for the router, `src/start.ts`, client/server config, and the
  generated route tree

See `skills/tanstack-start-project-structure/SKILL.md` for the index and `skills/tanstack-start-project-structure/rules/` for one file per rule.

### `choose-ui-design`

Chooses where each layer of a UI comes from before building it, then adapts
the pick to the project. Covers:

- reading the stack and classifying the surface (marketing vs product)
- finding references first: flows on Mobbin, product details on Kargul's
  swipe file
- one base system (shadcn/ui by default), with AlignUI Pro and Pro blocks
  rebuilt on it from their designs; sections from shadcnblocks, one
  signature effect from Aceternity UI or React Bits, bento layouts from
  bentogrids.com, backgrounds from grainient.supply
- mapping everything to project tokens and a motion budget

See `skills/choose-ui-design/SKILL.md` for the index and `skills/choose-ui-design/rules/` for one file per rule.

### `claude-delegate-and-budget`

Decides how an agent spends its context, tokens, and wall-clock: whether a
piece of work stays inline or goes to a subagent, which model tier the
subagent gets, and what effort (thinking) level each piece runs at. Covers:

- inline by default; delegate only for parallel independent chunks, to keep
  bulk reading out of the main context, or for an unanchored review
- briefing a subagent like a peer (goal, what is ruled out, pointers, scope,
  return shape), launching in the background, and never redoing or
  predicting delegated work
- Haiku for mechanical and verifiable work, Sonnet for bounded coding, Opus
  for judgment, Fable on request; cost judged per completed task; cheap
  fan-out with strong synthesis
- effort scaled to the cost of being wrong, low for narrow briefs, raised
  before irreversible steps and after repeated failures, and a one-line
  flag when the session setting does not fit
- a Claude Code mapping (`model` / `effort` on the Agent call, agent-file
  frontmatter, `ultrathink`, `/model`, `/effort`)

See `skills/claude-delegate-and-budget/SKILL.md` for the index and `skills/claude-delegate-and-budget/rules/` for one file per rule.

## License

MIT
