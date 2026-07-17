# Task 004: Seed ABOUT-ME.md

**Status:** done
**Depends on:** none
**Model tier:** cheap — content is fully specified below.

## Files
- Create: `ABOUT-ME.md`

## What to do

Per `CONTEXT.md`'s Implementation Decisions and this feature's `RESEARCH.md` (§3, resolved: single file, not a folder — no comparable second-brain implementation splits a single personal-context concern into a folder), create `ABOUT-ME.md` at project root, sibling to `CLAUDE.md`/`CLAUDE-WIKI.md`.

Create `ABOUT-ME.md` with exactly this content:

```markdown
# About Me

What Claude has learned about Alfonso — always-true, root-level personal context, structurally separate from the on-demand wiki (`wiki/shared/`, `wiki/claude-knowledge/`). Read on most sessions via `CLAUDE.md`'s `@import`, not looked up on demand like a wiki page.

Grown over time via the "grill me" interrogation process (used for both initial extraction and reconciliation — see `CLAUDE-WIKI.md`; the skill itself is a future feature and doesn't exist yet) and through ordinary conversation. Included in lint passes but held to a lighter bar than wiki pages, since it updates naturally through normal use rather than through deliberate ingestion.

---

Nothing captured yet.
```

## Interfaces
- Consumes: nothing.
- Produces: `ABOUT-ME.md` at the exact path `CLAUDE.md` (Task 006) `@import`s.

## Constraints
- No frontmatter (YAML) — the frontmatter schema in `CONTEXT.md` applies to wiki pages under `wiki/shared/`/`wiki/claude-knowledge/`; `ABOUT-ME.md` is explicitly outside the wiki.
- No placeholder/example personal content — stays genuinely empty until real conversation or a future grill-me pass populates it, consistent with the project's "no fake placeholder content" rule applied elsewhere (`index.md`, `log.md`).

## Verification
Run:
```
cat ABOUT-ME.md
```
Confirms: content matches exactly what's specified above.

## Evidence

`ABOUT-ME.md` created at project root, content verified via `cat ABOUT-ME.md` to match the specification exactly (no frontmatter, no placeholder content). Executor: haiku, DONE, exit code 0.
