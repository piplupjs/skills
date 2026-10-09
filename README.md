# skills

Agent Skills for [skills.sh](https://skills.sh) / `npx skills`-compatible
coding agents (Claude Code, Cursor, Codex, OpenCode, and 25+ others).

## Install

```bash
npx skills add piplupjs/skills --skill code-spacing
npx skills add piplupjs/skills --skill coding-principles
npx skills add piplupjs/skills --skill write-react-code
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

## License

MIT
