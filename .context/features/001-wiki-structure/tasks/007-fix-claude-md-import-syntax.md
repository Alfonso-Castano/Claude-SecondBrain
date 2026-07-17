# Task 007: Fix invalid @import syntax in CLAUDE.md

**Status:** done
**Depends on:** none (fix against an already-existing file)
**Model tier:** cheap — the fix is fully specified below; the executor's job is a one-line edit and verification.

## Files
- Modify: `CLAUDE.md` (project root)

## What to do

`.context/features/001-wiki-structure/REVIEW.md` found that `CLAUDE.md` line 5 uses invalid Claude Code import syntax: `@import ABOUT-ME.md`. This was independently verified against Anthropic's current Claude Code documentation (`code.claude.com/docs/en/memory`, fetched live during review): the real syntax is `@path` — the `@` is immediately followed by the path, with **no** `import` keyword and **no** space (e.g. the docs' own examples: `@README`, `@docs/git-instructions.md`).

As currently written, the parser reads `@import` as an attempt to import a nonexistent file literally named `import`, leaving `ABOUT-ME.md` as inert trailing text — it is never actually imported. This directly contradicts `CONTEXT.md`'s Implementation Decision that `ABOUT-ME.md` be `@import`ed directly so it loads into every session.

Change line 5 of `CLAUDE.md` from:
```
@import ABOUT-ME.md
```
to:
```
@ABOUT-ME.md
```

No other line in `CLAUDE.md` changes.

## Interfaces
- Consumes: nothing new — `ABOUT-ME.md` already exists at project root (Task 004).
- Produces: a `CLAUDE.md` whose import actually loads `ABOUT-ME.md` into every session, as originally specified.

## Constraints
- Do not change anything else in `CLAUDE.md` — the five plain-text pointers and overall structure already passed review untouched.
- Do not add a second `@import` or convert any of the five plain-text pointers into imports — only `ABOUT-ME.md` is meant to be imported (see `CONTEXT.md`'s Implementation Decisions and Global Constraints on keeping `CLAUDE.md` thin).

## Verification
Run:
```
cat CLAUDE.md
```
Confirms: line 5 reads exactly `@ABOUT-ME.md` (no `import` keyword, no space between `@` and the path), and no other line changed.

## Evidence

`CLAUDE.md` line 5 changed to exactly `@ABOUT-ME.md`, independently confirmed via direct read by the dispatching session — no `import` keyword, no space, no other line changed. Executor: haiku, DONE.
