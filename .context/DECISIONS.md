# Decisions Log

Running record of decisions that constrain future work. Newest first. Any future session or skill should check here before re-deciding something already settled.

## 2026-07-15 — No standalone roadmap

**Decision:** No `.context/ROADMAP.md` was created.
**Rationale:** The project's full arc before steady-state feature-loop use reduces to two already-named, already-sequenced features fully specified in `OVERVIEW.md`'s Context section — build the wiki structure and `CLAUDE-WIKI.md` schema (Feature #1), then re-ingest the two already-held sources through it. This is ordinary `/feature` sequencing, not phase decomposition; a separate roadmap would only restate what `OVERVIEW.md` and `.context/research/SUMMARY.md` already say.
**Made during:** Project initialization

## 2026-07-15 — Schema file name and location

**Decision:** The dedicated schema file (governing ingestion/query/lint workflows, new-page-vs-edit rule, shared/claude-knowledge convention, propose-then-confirm) is `CLAUDE-WIKI.md` at the project root.
**Rationale:** Sibling to `CLAUDE.md`, keeps the router/detail split visible at a glance. Decided live during initialization rather than deferred to Feature #1's own discuss/plan loop, per Alfonso's preference.
**Made during:** Project initialization

## 2026-07-15 — Repo location confirmed

**Decision:** `Claude-SecondBrain` (this repo, at `c:\Users\alfon\SecondBrain\Claude-SecondBrain`) is the final home for the project.
**Rationale:** Confirmed settled by Alfonso at initialization, though explicitly open to change later if a real reason emerges — not treated as permanently locked.
**Made during:** Project initialization

## 2026-07-15 — Research-surfaced gaps deferred to Feature #1, not resolved here

**Decision:** Concrete gaps found during domain research (page-level YAML frontmatter template, anti-`[[wikilink]]` rule, earned-not-mechanical `shared`/`claude-knowledge` pairing, a concrete lint checklist, stakes-differentiated propose-then-confirm, reconciliation requiring Alfonso's own counter-reasoning rather than accept/reject) are recorded in `.context/research/SUMMARY.md` for Feature #1's discuss/plan loop to pick up, not decided or written into `CLAUDE-WIKI.md` during this initialization.
**Rationale:** Per the project's standing principle, decisions this substantive about the wiki's actual operating rules stay human-reviewed through the full feature loop rather than being defaulted by an init script.
**Made during:** Project initialization
