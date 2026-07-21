# dyslexia-friendly-code

A skill that shapes the code an AI assistant writes so a reader with dyslexia can scan it without losing their place. It favours vertical layout over long horizontal lines, keeps names visually distinct, and adds a consistent file header. It triggers on any coding task, not just when asked.

## Why

Dyslexia is a common, lifelong difference in how the brain processes written language — not a matter of intelligence or effort. It makes reading slower and mistracking a line or transposing similar shapes easier, and dense material tires the eye quickly. Layout that reduces how much the eye has to scan and track directly reduces that load. Every rule in the skill exists for that reason.

## What it does

The skill tells the assistant to:

1. Put one property per line in any object literal with 2+ properties (arrays of records, JSON, config).
2. Break long arrays and parameter lists so each item sits on its own line.
3. Use visually distinct names, and prefer camelCase — case changes give each word a shape and a boundary the eye can catch.
4. Keep indentation and alignment consistent; never mix tabs and spaces.
5. Separate logical chunks with blank lines.
6. Put comments above the code, not trailing.
7. Never write comment blocks except a file's licence header.
8. Open every file with a header naming the file, with the licence under it if there is one.

When reformatting existing code it only changes layout — never keys, values, or logic — and verifies afterwards with the type checker, linter, and JSON validation.

Full detail, with good/bad examples for each rule, is in `SKILL.md`.

## Files

`SKILL.md` is the skill itself. `dyslexia-friendly-code.skill` is the same thing zipped for one-click install.

## Install

In Cowork or Claude Code, add the skill through Settings → Capabilities (or open the `.skill` bundle and choose Save skill). Once installed it loads automatically on coding tasks; you can also invoke it by name.

## Other assistants

The root `SKILL.md` targets Claude. `codex/SKILL.md` is a Codex-tuned variant for ChatGPT's Codex — shorter and action-oriented, with explicit "layout only" safeguards. For a repository, drop it at `.codex/skills/dyslexia-friendly-code/SKILL.md`, or adapt its rules into an `AGENTS.md` to apply repo-wide.

## Licence

MIT — see `LICENSE`.
