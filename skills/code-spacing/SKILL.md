---
name: code-spacing
description: Vertical whitespace (blank lines) for readable code. Use when writing, generating, refactoring, reviewing, or formatting code in any language, or when the user asks about blank lines, code readability, spacing rules, or linter/formatter config (Prettier, ESLint, Black, PEP 8, .editorconfig).
---

# Code Spacing

**One blank line = one conceptual boundary.** Ask: "does the code above finish a thought different from what follows?" If yes, blank line. If steps in the same thought, keep tight. Every rule below is this principle applied.

## Universal rules

1. **Group by logical step.** Blank lines separate stages (validate → transform → write). Related setup feeding one call stays tight.
2. **Never pad inside a block.** No blank line after `{`/`(`/`[`/`:` or before `}`/`]`/dedent.
   ```js
   // bad                          // good
   function bar() {                function bar() {
                                 
     console.log(foo);               console.log(foo);
                                 
   }                               }
   ```
3. **One blank line max.** Collapse consecutive blanks to one. (Exceptions: Python top-level defs — see below.) Enforced by `no-multiple-empty-lines`, `E303`.
4. **No leading/trailing blanks.** No blank as first/last line of a file or block. File ends with one newline.
5. **Imports separated.** One blank line between imports and code. Keep import groups internally tight unless the language convention uses sub-groups (e.g. Python stdlib / third-party / local — one blank between groups).
6. **Section comments get a blank before, not after.** Attach to the code they explain.
   ```js
   doStuffA();
   doStuffB();

   // Handle empty queue.
   if (queue.isEmpty()) { ... }
   ```
7. **Return/throw/break — blank before when not the only statement.** Distinct "wrapping up" thought; skip for trivial one-liners.
8. **Parallel one-liners stay tight.** Runs of simple, repetitive lines (constants, stubs, mirrored assignments) — no blanks; they'd imply a break that isn't there.
9. **Match the file.** When editing, mirror existing conventions. Impose defaults only for new files or explicit cleanup requests.

## Between declarations

| Context | Spacing |
|---|---|
| Top-level functions/classes | 1 blank line (C-family, JS/TS); **2** in Python (PEP 8) |
| Methods inside a class | 1 blank line (all languages) |
| Fields → first method | 1 blank line |
| Logical groups of functions | Extra blank line for rare, real section breaks |

## Horizontal spacing

- One space after commas, around `a + b`, after `if (`/`while (` — not between `foo` and `()` .
- No trailing whitespace. Consistent indent (2 or 4 spaces, or tabs) — never mix.

## Language notes

| Language | Between top-level defs | Notes |
|---|---|---|
| Python | 2 blank lines (PEP 8) | 1 between methods; sparse blanks inside functions |
| JavaScript/TypeScript | 1 | ESLint `padded-blocks: off`, max 1 empty line |
| Java | 1 | Google Style: 1 between members; grouping inside methods OK |
| Go | 1 | Defer to `gofmt` |
| C / C++ | 1 | Blank line before/after function defs |
| Rust | 1 | Defer to `rustfmt` |
| SQL | 1 | Separate CTEs; major clauses (SELECT/FROM/WHERE) as blocks |

If a formatter (Prettier, Black, gofmt, rustfmt, clang-format) or `.editorconfig` exists, defer to it.

## Workflow

- **When generating:** apply automatically — don't wait to be asked. Cramped/over-padded code is a readability defect.
- **After drafting:** one blank-line pass — every blank is a real boundary? No runs of 2+? No block-edge padding?
- **When reviewing:** explain with reasoning ("these three lines are one setup step — the blank implies a break that isn't there"), not just rule numbers.
