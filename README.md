# skills

Agent Skills for [skills.sh](https://skills.sh) / `npx skills`-compatible
coding agents (Claude Code, Cursor, Codex, OpenCode, and 25+ others).

## Install

```bash
npx skills add piplupjs/skills --skill code-spacing
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

See `skills/code-spacing/SKILL.md` for the full skill.

## License

MIT
