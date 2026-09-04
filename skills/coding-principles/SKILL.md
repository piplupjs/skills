---
name: coding-principles
description: Apply core software engineering principles — DRY, SOLID, YAGNI, KISS, and related design heuristics — whenever writing, reviewing, refactoring, or reasoning about code. Use this skill for any coding task: new features, bug fixes, refactors, code review, or architecture/design discussions, regardless of language or framework. It governs how code should be structured (not what it should do), so it applies even when the user doesn't mention "clean code," "best practices," or these principles by name.
---

# Coding Principles

A skill for writing and reviewing code the way a disciplined senior engineer would: simple, well-factored, and no more complex than the problem requires.

## Overview

These principles exist in tension with each other. DRY and SOLID push toward more abstraction; YAGNI and KISS push back toward less. Good engineering is not maximizing any single principle — it's picking the right amount of structure for the problem actually in front of you. Treat every principle below as a **default heuristic**, not a rule to apply mechanically. When two principles conflict, say so and explain the tradeoff rather than silently picking one.

**Priority order when principles conflict:** correctness > clarity/simplicity (KISS, YAGNI) > non-repetition (DRY) > extensibility (SOLID, OCP). A working, readable, slightly-repetitive solution beats a broken or unreadable "elegant" one every time.

## Core principles

### YAGNI — You Aren't Gonna Need It

Don't build for hypothetical future requirements. Implement what's needed now, in a way that's easy to extend later — not the extension itself.

- Don't add config options, plugin systems, abstract base classes, or generic parameters for a single current use case.
- Don't add a database/cache/queue "in case we need to scale" before there's a concrete need.
- When the user's request implies future needs ("we'll probably add X later"), ask or note the assumption briefly rather than pre-building X now.
- Red flag: a function taking a `strategy` or `mode` parameter that only ever has one caller with one value.

### KISS — Keep It Simple

Prefer the straightforward solution over the clever one. Optimize for the next reader, not for showing off language features.

- Prefer a plain loop over a dense one-liner that requires unpacking three chained higher-order functions, unless the terse form is genuinely idiomatic and clear in that language.
- Avoid premature abstraction: three lines duplicated twice is often better than a poorly-named helper that obscures what's happening.
- Naming, structure, and control flow should make the code's intent legible without needing comments to explain *what* it does (comments should explain *why*, when needed).

### DRY — Don't Repeat Yourself

Every piece of knowledge (a business rule, a calculation, a schema) should have a single, authoritative representation in the codebase.

- DRY is about **duplicated knowledge**, not duplicated *text*. Two pieces of code that look similar but represent independent decisions (e.g., two validation rules that coincidentally have the same regex today) are not a DRY violation — don't couple them just because they currently match.
- Apply the "rule of three": tolerate one or two instances of similar code; extract a shared abstraction once a third appearance confirms the pattern is real and stable.
- Extracting too early, before the shared shape is clear, tends to produce a leaky abstraction that's harder to change than the duplication it replaced — this is where DRY and YAGNI must be balanced.
- Applies to logic and data (constants, magic numbers, schemas), not just literal code — e.g., a validation rule should live in one place even if it's checked in three layers (client, API, DB).

### SOLID

Apply these primarily at module/class/function-boundary granularity — they're about how responsibilities are divided, not about mandating specific patterns (factories, interfaces, DI containers) everywhere.

- **S — Single Responsibility**: A unit of code (function, class, module) should have one reason to change. If describing what a function does requires "and," consider splitting it. Don't fragment trivial code into needless layers to satisfy this on paper — a 5-line function doesn't need to become three.
- **O — Open/Closed**: Code should be extensible without modifying existing, working, tested code — typically via composition, interfaces, or configuration rather than editing a growing `if/elif/switch` chain. Don't over-apply this: if there's only one variant today and no evidence a second is coming, a simple conditional is fine (see YAGNI).
- **L — Liskov Substitution**: A subtype must be usable anywhere its base type is expected without breaking correctness — no narrowing accepted inputs, widening thrown exceptions, or violating the base type's invariants. If a subclass has to throw `NotImplementedError` on an inherited method, that's a sign the hierarchy is wrong, not that LSP needs an exception.
- **I — Interface Segregation**: Don't force callers to depend on methods they don't use. Prefer several small, focused interfaces/protocols over one large one. Don't fragment a genuinely cohesive interface just to hit this in the abstract.
- **D — Dependency Inversion**: High-level logic should depend on abstractions (interfaces, protocols, injected dependencies), not directly on low-level implementation details — especially for things that are slow, external, or likely to be swapped or mocked (databases, HTTP clients, filesystems, third-party SDKs). Don't introduce an interface for a dependency that will only ever have one implementation and isn't being tested in isolation — that's YAGNI territory.

## Supporting heuristics

Use these to round out judgment; they're secondary to the principles above but frequently relevant.

- **Separation of Concerns**: Keep distinct responsibilities (e.g., business logic, data access, presentation/formatting, I/O) in distinct layers so each can change independently.
- **Composition over Inheritance**: Prefer building behavior by combining small, independent pieces over deep inheritance hierarchies. Reach for inheritance only for genuine "is-a" relationships with stable shared behavior.
- **Law of Demeter (principle of least knowledge)**: A unit of code should only talk to its immediate collaborators, not reach through them (avoid `a.getB().getC().doThing()` chains) — such chains tightly couple callers to internal structure they shouldn't know about.
- **Fail Fast**: Validate inputs and invariants early and raise clear errors immediately, rather than letting bad state propagate silently into a confusing failure later.
- **Command-Query Separation**: A function should either perform an action (command) or return information (query), not both — a function called `getUser()` shouldn't also mutate state.
- **Explicit over Implicit**: Prefer explicit parameters, return types, and error handling over hidden globals, implicit type coercion, or silent fallbacks that mask bugs.

## Applying this in practice

**When writing new code:**
1. Solve the actual current requirement first — resist speculative generalization (YAGNI).
2. Structure it clearly: small functions/classes with one clear job, sensible names, minimal nesting (KISS, SRP).
3. Don't extract shared abstractions preemptively; wait for real duplication of *knowledge*, not just similar-looking code (DRY, rule of three).
4. Depend on abstractions only where there's a real reason to (multiple implementations, need to mock in tests) — not by default (DIP).

**When reviewing or refactoring existing code**, call out violations concretely rather than abstractly — name the principle, show the smell, and propose a specific fix:
- Copy-pasted logic representing the same business rule in 3+ places → DRY: extract a shared function.
- A class/function doing several unrelated things → SRP: split along the seams.
- A growing `switch`/`if-elif` chain that gets a new branch every time a new "type" is added → OCP: consider polymorphism or a lookup table instead.
- Deep method chains reaching into other objects' internals → Law of Demeter.
- Unused config flags, generic parameters with one caller, abstract classes with one subclass → YAGNI: simplify or inline.
- Clever one-liners that take longer to parse than a plain loop would → KISS.

**When principles conflict**, state the tradeoff explicitly instead of picking silently — e.g., "This introduces an interface for DIP, but there's only one implementation and no tests mocking it yet, so I'd lean YAGNI and keep it concrete until a second implementation shows up."

**Don't be dogmatic.** These are aids to writing maintainable software, not a checklist to satisfy for its own sake. A junior engineer over-applies SOLID and DRY until the code is a maze of indirection; a senior engineer knows when three lines of duplication is the right call. Aim for the latter.
