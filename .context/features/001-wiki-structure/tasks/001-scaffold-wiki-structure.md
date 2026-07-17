# Task 001: Scaffold wiki directory structure and seed navigation files

**Status:** done
**Depends on:** none
**Model tier:** cheap — every file's exact content is specified below; the executor's job is creating the tree and transcribing content, then verifying with `ls`/`cat`.

## Files
- Create: `raw/.gitkeep`
- Create: `wiki/shared/.gitkeep`
- Create: `wiki/claude-knowledge/.gitkeep`
- Create: `projects/.gitkeep`
- Create: `index.md`
- Create: `log.md`

## What to do

Git does not track empty directories, and `CONTEXT.md`/`OVERVIEW.md` require `raw/`, `wiki/shared/`, `wiki/claude-knowledge/`, and `projects/` to exist as genuinely empty placeholders (no fake/example content — Alfonso-confirmed). Create each with a `.gitkeep` file (empty file, zero bytes) so the folder is tracked.

`OVERVIEW.md` lists `raw/`, `wiki/`, `index.md`, and `log.md` as four parallel, top-level components — `index.md` and `log.md` belong at project root, sibling to `CLAUDE.md`, not nested inside `wiki/`.

Create `index.md` (project root) with exactly this content:

```markdown
# Index

Unified catalog of every page across `wiki/shared/` and `wiki/claude-knowledge/`, folder-tagged per entry. Read this first for any query — drill into individual pages only for what's relevant. Never load the whole wiki into context.

**Size trigger:** if this file exceeds ~150–200 entries or ~3–4k tokens, flag it during the next lint pass — that's the point at which index-first retrieval starts to strain.

---

No pages yet.
```

Create `log.md` (project root) with exactly this content:

```markdown
# Log

Append-only record of every wiki operation — ingestion, lint, reconciliation, and ad-hoc filing. Newest entry first (prepend, don't append to the bottom) so recent activity is visible without scrolling.

**Format:** one line per operation —
`YYYY-MM-DD | <ingest|lint|reconcile|file> | <short description> | <files touched>`

**Rotation trigger:** past ~500 entries, rotate this file to `log-YYYY.md` (starting a fresh `log.md`) and check for this during lint passes — mirrors `index.md`'s own size trigger.

---

No operations logged yet.
```

## Interfaces
- Consumes: nothing.
- Produces: the directory tree and two seeded navigation files (`index.md`, `log.md` at project root) that `CLAUDE.md` (Task 006) points to and that `CLAUDE-WIKI.md` (Task 005) describes the workflows around.

## Constraints
- Do not add any example/placeholder wiki pages to `wiki/shared/` or `wiki/claude-knowledge/` — they must stay genuinely empty (only the `.gitkeep`).
- Do not write anything into `raw/` — it stays empty until Feature #2's ingestion pass.
- `log.md`'s content is a seed/header only — do not add example log lines.

## Verification
Run:
```
ls raw wiki wiki/shared wiki/claude-knowledge projects
cat index.md
cat log.md
```
Confirms: all four directories exist with a `.gitkeep`; `index.md` and `log.md` (project root) contain exactly the content above (diff by eye against this task file).

## Evidence

All four directories (`raw/`, `wiki/shared/`, `wiki/claude-knowledge/`, `projects/`) created with `.gitkeep`; `index.md` and `log.md` created at project root, content verified via direct read to match specification exactly. Executor: haiku, DONE, exit code 0.
