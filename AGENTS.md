# AGENTS.md

## Skills — Vercel + skills.sh (agentskills.io) compliance

This repo is `npx skills`-compatible, published via `skills.sh` (`piplupjs/skills`). Skills: `code-spacing`, `coding-principles`, `write-react-code`.

**Frontmatter (required + recommended):**
- `name`: kebab-case, must match folder name exactly
- `description`: 1–3 sentences, sentence 1 = WHAT, sentence 2 = WHEN with `Use when...` and quoted user phrases (max 1024 chars). Dense triggers: `"cramped"`, `"clean code"`, `DRY/SOLID` etc.
- `when_to_use: |` — 4–5 bullets (natural triggers + `Do NOT use for:` boundary). Supported by Claude Code/Codex/OpenClaw; improves activation beyond description alone
- `license: MIT` + `metadata: {author: piplupjs, version: "1.0.0"}` — for skills.sh discoverability (Vercel template parity)

**Body (Vercel guidelines: Be specific. Include examples. Use numbered steps. Set boundaries. Keep focused):**
- Start with Workflow numbered steps (generate → pass → review)
- 1–2 concrete before/after code examples per skill
- Tables for scannability (declaration spacing, SOLID, heuristics)
- Boundaries: explicit `Do NOT use for` in `when_to_use` + body
- Keep focused: one domain per skill, <5000 chars body, imperative voice

**Validation:** `name` matches folder, description under limit, YAML `---` delimiters correct, file is `SKILL.md`. Check with `skills-ref validate` if available.

**README:** Install section must list `npx skills add piplupjs/skills --skill <name>` for each skill + `--list` hint.
