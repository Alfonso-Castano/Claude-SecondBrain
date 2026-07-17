# Project State

## Reference

See: .context/OVERVIEW.md
See: .context/research/SUMMARY.md

**Core value:** A durable, cross-venture knowledge base that gives Alfonso a genuinely knowledgeable, independent thinking partner — without ever letting AI make strategic or creative decisions for him.

## Current Position

Status: Feature #1 (Wiki Structure) complete, passed `/feature-verify`, and **merged into `main`** (merge commit `6438af0`). A post-merge review against Alfonso's stated intent then found one real gap and three items worth recording — all addressed directly on `main` rather than requiring a new feature cycle (see `.context/DECISIONS.md`'s 2026-07-17 entries for full detail).

What exists on `main`: `raw/`, `wiki/shared/`, `wiki/claude-knowledge/`, `projects/` folders; `index.md` and `log.md` seeded empty; `CLAUDE-WIKI.md` — the full operating schema (frontmatter template, ingestion/query/lint workflows, new-page-vs-edit rule, earned-not-mechanical pairing, anti-wikilink rule, propose-then-confirm with the write-only-gating boundary, the devil's-advocate pushback design, and — added post-merge — an explicit depth-preservation rule in the ingestion workflow, §4); `CLAUDE.md` as a thin router that correctly `@imports` `ABOUT-ME.md`; `ABOUT-ME.md` seeded as a single root-level file (confirmed post-merge to be a deliberate split from `OVERVIEW.md`, not an accidental gap); markdown tooling; and automemory disabled and verified scoped to this repo.

**Two things flagged, not yet resolved (see DECISIONS.md):** (1) whether Feature #2 should wait for the "grill me" skill to exist or whether `CLAUDE-WIKI.md` needs an interim ambiguous-content rule before it does — genuinely open, Alfonso's call; (2) the devil's-advocate design and several other `CLAUDE-WIKI.md` mechanics (citation-chain checks, earned pairing, size/rotation triggers) are provisional, reasoned from first principles but not yet tested against a real ingestion pass.

Last activity: 2026-07-17 — post-merge amendments to `CLAUDE-WIKI.md` and `DECISIONS.md` (depth-preservation fix, open sequencing question, provisional-design flag, ABOUT-ME.md/OVERVIEW.md split confirmation).

## Next Action

Start Feature #2 through `/feature-discuss`: re-ingest the two already-held sources — Hormozi's *$100M Offers* and a negotiation book — through the now-existing wiki workflow defined in `CLAUDE-WIKI.md`. **Before ingestion actually starts, `/feature-discuss` must explicitly raise and resolve the open "grill me" sequencing question** (DECISIONS.md, 2026-07-17) rather than silently defaulting to either option.
