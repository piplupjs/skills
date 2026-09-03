---
name: code-spacing
description: How to use vertical whitespace (blank lines) between lines of code for good developer experience and readability. Use this whenever writing, generating, refactoring, reviewing, or formatting code in any language — including single functions, full files, diffs, and code review comments about style. Also use when the user asks about blank line conventions, code readability, "why does my code look cramped/messy", spacing rules, or requests a linter/formatter config (e.g. .editorconfig, ESLint padding-line-between-statements, Prettier, PEP 8 blank-line rules, Black). Applies to code Claude writes itself, not just code it's asked to critique — don't wait for the user to mention spacing explicitly before applying these rules to generated code.
---

# Code Spacing

Vertical whitespace is punctuation for code. A blank line is a paragraph break: it tells
the reader "the previous thought is finished, a new one starts here." Too few blank lines
and everything reads like a wall of text; too many and the reader loses the thread between
related lines. Both failure modes slow a reviewer down and hide bugs. This skill gives
concrete rules for getting it right, plus the reasoning so you can extrapolate to cases
not explicitly covered.

## The core principle

**One blank line = one conceptual boundary.** Before adding or removing a blank line, ask:
"does the code above this point finish a thought that's different from what follows?" If
yes, a blank line belongs there. If the lines are steps in the same thought, keep them
together with no blank line between them.

This one question resolves almost every spacing decision below. The rest of this skill is
that principle applied to specific, common situations.

## Universal rules (apply in every language)

1. **Group by logical step, not by arbitrary length.** Within a function, blank lines
   separate stages of the work — e.g. "validate input" / "transform data" / "write result."
   Related statements that build toward one outcome (a chain of variable setup that all
   feeds one call, for instance) stay tight with no blank lines between them.

2. **Never pad the inside of a block.** No blank line immediately after `{`, `(`, `[`, a
   `:` that opens a suite, or immediately before the closing brace/bracket/dedent. A block
   with breathing room at its edges but nothing meaningfully separated inside just looks
   unfinished.

   ```
   // bad
   function bar() {

     console.log(foo);

   }

   // good
   function bar() {
     console.log(foo);
   }
   ```

3. **One blank line, not a rolling lawn.** A single blank line is a paragraph break; two or
   more in a row (outside of language conventions that explicitly call for two, like
   Python's top-level def/class spacing) just adds scrolling. Collapse consecutive blank
   lines to exactly one. Most linters enforce this (`no-multiple-empty-lines` in ESLint,
   `E303` in pycodestyle) — treat it as a hard rule even without a linter present.

4. **No trailing blank lines at the very start or end of a file**, and no blank line as the
   very first or very last line inside a block. Files should end with exactly one newline
   (no extra blank lines), and most style guides forbid a blank line as the first line of a
   file too.

5. **Separate imports/includes from the code that uses them** with one blank line, and keep
   import groups internally blank-line-free unless the language convention calls for
   sub-groups (e.g. Python's stdlib / third-party / local convention, separated by one
   blank line each).

6. **A comment that introduces a new section gets a blank line before it** (not after) so
   it visually attaches to the code it explains, not the code above it.

   ```
   doStuffA();
   doStuffB();

   // Now handle the edge case where the queue is empty.
   if (queue.isEmpty()) {
     ...
   }
   ```

7. **Return/throw/break statements that aren't the only statement in a block** often
   deserve a blank line before them — they're a distinct "wrapping up" thought, separate
   from the logic that decided the outcome. Don't apply this mechanically to trivial
   one-line functions.

8. **Related one-liners can be packed tightly.** A run of simple, parallel statements
   (constant declarations, a set of dummy/stub implementations, simple assignments that
   mirror each other) reads better with no blank lines between them — the blank line would
   imply a break in logic that doesn't exist. This is the explicit exception to rule 1 for
   truly parallel, repetitive lines.

9. **Match the surrounding file.** If you're editing existing code, mirror its existing
   spacing conventions even if they differ slightly from the defaults below — consistency
   within a file beats a "more correct" outside convention. Only impose these defaults when
   writing new files or when the user asks you to clean up/reformat.

## Structural spacing (between declarations)

These are the most consistent rules across style guides, and where being wrong is most
visible in a diff or review:

- **Between top-level functions/classes:** one blank line in most C-family languages and
  JS/TS; **two** blank lines in Python (PEP 8) between top-level `def`/`class`.
- **Between methods inside a class:** one blank line, in essentially every language.
- **Between a class's fields/properties and its first method:** one blank line.
- **Between logically distinct groups of related functions:** an extra blank line is
  acceptable to mark a bigger seam, but don't do this "sparingly" caveat lightly — it's
  meant for rare, real section breaks, not routine spacing.

## Horizontal spacing (brief — this skill is mainly about blank lines)

Vertical whitespace is the focus here, but a few horizontal rules matter for the same
"reads like punctuation" reason and are worth enforcing alongside blank lines:

- One space after commas, around binary operators (`a + b`, not `a+b`), and after control
  keywords (`if (`, `while (`) — but not between a function/method name and its opening
  parenthesis (`foo()`, not `foo ()`). This distinguishes calls from keywords at a glance.
- No trailing whitespace at the end of any line.
- Indent with a consistent unit (commonly 2 or 4 spaces, or a tab set to match) — never mix
  tabs and spaces in one file.

## Language quick-reference

When the language is known, prefer its dominant community convention over the generic
defaults above where they conflict:

| Language | Between top-level defs | Notes |
|---|---|---|
| Python | 2 blank lines (PEP 8) | 1 blank line between methods in a class; blank lines inside functions used sparingly to mark logical sections |
| JavaScript/TypeScript | 1 blank line | Airbnb/ESLint: no padding inside blocks (`padded-blocks`), blank line after a block before the next statement, max 1 consecutive empty line |
| Java | 1 blank line | Google Java Style: 1 blank line between members; blank lines allowed for logical grouping within a method body |
| Go | 1 blank line | `gofmt` normalizes most of this automatically — defer to it rather than hand-formatting |
| C / C++ | 1 blank line | Blank line before/after function definitions; blank lines to separate logical segments within a function |
| Rust | 1 blank line | `rustfmt` normalizes most of this — defer to it |
| SQL | 1 blank line | Separate CTEs, and major clauses in long queries (SELECT/FROM/WHERE/GROUP BY) can each start a visually separated block |

If the project has a formatter (Prettier, Black, gofmt, rustfmt, `clang-format`) or an
`.editorconfig`, defer to it over these defaults — the point of this skill is to make good
choices when no automated formatter is configured, or when writing new code before it's
been run through one.

## Applying this while writing code

- Default to these rules automatically when generating code — don't wait to be asked about
  spacing. Cramped or over-padded code is a real readability defect, same as bad naming.
- After drafting a function or file, do one pass specifically for blank lines: does every
  blank line correspond to a real conceptual boundary? Are there two-plus in a row
  anywhere? Is the inside of any block padded at its edges? Fix in that pass rather than
  spacing as you go, since it's easier to see paragraph structure once the content exists.
- When asked to review or clean up someone else's code for style, call out spacing issues
  using the same reasoning ("these three lines are one setup step, the blank line between
  them implies a break that isn't there") rather than just citing a rule — it helps the
  request-maker apply the same judgment next time.
