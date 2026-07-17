# Task 006: Write CLAUDE.md (thin router)

**Status:** done
**Depends on:** 004 (`ABOUT-ME.md` must exist — this file `@import`s it directly), 005 (`CLAUDE-WIKI.md` must exist — this file points to it)
**Model tier:** cheap — the exact list of pointers/imports is fully specified below (from `CONTEXT.md`'s Implementation Decisions); no judgment required beyond correct `@import` syntax.

## Files
- Create: `CLAUDE.md` (project root)

## What to do

Create `CLAUDE.md` at project root — a new file, thin router only, per `CONTEXT.md`'s Implementation Decisions ("`CLAUDE.md` router scope") and the Global Constraint that it must stay thin (router/imports only, never inline operating rules, since it loads into every session automatically and anything written directly into it is a fixed cost on every session).

Content must:
- Point to (as plain references, not necessarily `@import`s — these are read on demand, not every session): `.context/OVERVIEW.md`, `.context/STATE.md`, `CLAUDE-WIKI.md`, `.context/DECISIONS.md`, `index.md` (project root — `OVERVIEW.md` lists `index.md` as a top-level component, not nested under `wiki/`).
- `@import` `ABOUT-ME.md` directly (loaded into every session, same mechanism as how `OVERVIEW.md`/`STATE.md` would be — About Me is meant to be read on most sessions, per the external review's precedent recorded in `.context/DECISIONS.md`'s 2026-07-17 entry).

Suggested content (adjust formatting/wording as needed, but keep every pointer and the one `@import`):

```markdown
# Claude — Second Brain Router

This file is intentionally thin — router only, no operating rules inline. It loads into every session automatically.

@import ABOUT-ME.md

## Where things live

- Project context and scope: `.context/OVERVIEW.md`
- Current state / next action: `.context/STATE.md`
- Wiki operating rules (ingestion, query, lint, propose-then-confirm, pushback design): `CLAUDE-WIKI.md`
- Decision history: `.context/DECISIONS.md`
- Wiki catalog (read first for any query): `index.md`
```

## Interfaces
- Consumes: `ABOUT-ME.md` (Task 004) and `CLAUDE-WIKI.md` (Task 005) both existing at the paths referenced/imported here.
- Produces: the project's session entry point — nothing downstream in this feature depends on it, but every future session will load it.

## Constraints
- Do not inline any operating rule, workflow detail, or schema content here — that all belongs in `CLAUDE-WIKI.md` (Task 005). If you find yourself writing more than a pointer sentence per item, that content belongs elsewhere.
- Do not `@import` anything except `ABOUT-ME.md` — the other four references are read-on-demand pointers, not fixed-cost-every-session imports (that distinction is the entire point of keeping this file thin).

## Verification
Run:
```
cat CLAUDE.md
```
Confirms: exactly one `@import` line (`ABOUT-ME.md`), plus plain-text pointers to `.context/OVERVIEW.md`, `.context/STATE.md`, `CLAUDE-WIKI.md`, `.context/DECISIONS.md`, `index.md`, and no inline operating-rule content.

## Evidence

`CLAUDE.md` created at project root, independently read by the dispatching session and confirmed to contain exactly one `@import` (`ABOUT-ME.md`) plus five plain-text pointers to `.context/OVERVIEW.md`, `.context/STATE.md`, `CLAUDE-WIKI.md`, `.context/DECISIONS.md`, `index.md`, with no inline operating-rule content. Executor: haiku, DONE, exit code 0.
