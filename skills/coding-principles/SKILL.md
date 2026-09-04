---
name: coding-principles
description: Software design principles (DRY, SOLID, YAGNI, KISS) for writing, reviewing, refactoring, or designing code. Use for any coding task regardless of language — features, bug fixes, refactors, code review, or architecture discussions. Apply even when the user doesn't say "clean code" or "best practices".
---

# Coding Principles

Simple, well-factored, and no more complex than the problem requires.

Principles conflict — DRY/SOLID push toward abstraction, YAGNI/KISS push back. Good engineering picks the right amount of structure for the actual problem. Treat each as a heuristic, not a rule. When two conflict, name the tradeoff.

**Priority:** correctness > clarity/simplicity (KISS, YAGNI) > non-repetition (DRY) > extensibility (SOLID). A working, readable, slightly repetitive solution beats broken or unreadable "elegance."

## YAGNI — You Aren't Gonna Need It

Don't build for hypothetical requirements. Solve what's needed now in an extendable way — not the extension itself.

- No config options, plugin systems, abstract bases, or generic params for one use case.
- No DB/cache/queue "in case we scale" without concrete need.
- "We'll probably add X later" → note the assumption, don't pre-build X.
- Smell: `strategy`/`mode` param with one caller and one value.

## KISS — Keep It Simple

Straightforward > clever. Optimize for the next reader.

- Plain loop > dense chained one-liner (unless idiomatic and clear).
- Three duplicated lines twice > poorly-named helper that obscures intent.
- Names, structure, and flow should convey *what* without comments (comments explain *why*).

## DRY — Don't Repeat Yourself

One authoritative representation per piece of knowledge — not per text match.

- **Knowledge, not text.** Two validations with the same regex today but independent reasons ≠ DRY violation.
- **Rule of three:** tolerate 1–2 duplications; extract on the 3rd when the pattern is stable.
- Extracting too early creates a leaky abstraction harder to change than the duplication.
- Applies to logic *and* data (constants, schemas) — e.g. one validation rule, checked in client/API/DB.

## SOLID

At module/class/function boundaries — how responsibilities are split, not a mandate for factories/DI everywhere.

| Principle | Rule | Don't over-apply |
|---|---|---|
| **S** Single Responsibility | One reason to change; "and" in the description → consider splitting. | A 5-line function doesn't need three layers. |
| **O** Open/Closed | Extend without editing tested code — via composition/interfaces/config over growing `if`/`switch` chains. | One variant today → simple conditional is fine (YAGNI). |
| **L** Liskov Substitution | Subtype usable anywhere its base is expected; no narrowed inputs, widened exceptions, or broken invariants. | `NotImplementedError` on inherited method → hierarchy is wrong. |
| **I** Interface Segregation | Small, focused interfaces over one fat one. | Don't fragment a genuinely cohesive interface. |
| **D** Dependency Inversion | High-level logic depends on abstractions (injected DB/HTTP/FS clients), not concretions — for things that are slow, external, or swappable. | One impl, not mocked in tests → interface is YAGNI. |

## Heuristics

| Heuristic | Guideline |
|---|---|
| Separation of Concerns | Business logic, data access, presentation, I/O in distinct layers. |
| Composition over Inheritance | Combine small pieces; inherit only for stable "is-a" + shared behavior. |
| Law of Demeter | Talk to immediate collaborators only — avoid `a.getB().getC().doThing()` chains. |
| Fail Fast | Validate early, raise clearly — don't let bad state propagate. |
| Command-Query Separation | A function does an action *or* answers a question, not both (`getUser()` shouldn't mutate). |
| Explicit over Implicit | Explicit params/types/errors > hidden globals, coercion, silent fallbacks. |

## Applying

**Writing new code:**
1. Solve the current requirement first (YAGNI).
2. Small units, one job, clear names, minimal nesting (KISS, SRP).
3. Don't extract shared abstractions preemptively — wait for real *knowledge* duplication (rule of three).
4. Depend on abstractions only with a reason (multiple impls, need to mock) — not by default (DIP).

**Reviewing / refactoring** — name the principle, show the smell, propose a fix:

| Smell | Fix |
|---|---|
| Same business rule copy-pasted 3+ places | DRY → extract shared function |
| Class/function doing unrelated things | SRP → split along seams |
| Growing `switch`/`if-elif` per new type | OCP → polymorphism or lookup table |
| `a.getB().getC().doThing()` chains | Demeter → expose behavior, not internals |
| Unused flags, generic params with one caller, abstract class with one subclass | YAGNI → simplify/inline |
| Clever one-liner slower to parse than a loop | KISS → plain loop |

**When principles conflict**, state it: *"This adds an interface for DIP, but there's one impl and no test mocking it — lean YAGNI, keep concrete until a second use appears."*

Don't be dogmatic — a junior over-applies SOLID/DRY into indirection; a senior knows when three duplicated lines is the right call.
