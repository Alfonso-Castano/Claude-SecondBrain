# Second Brain

## What This Is

A persistent, file-based knowledge system that Claude Code reads from and writes to directly — no separate frontend, no database. It's modeled on Andrej Karpathy's raw/wiki method (raw source material in, an AI-organized interlinked wiki out) and built to function as a genuinely knowledgeable executive assistant or co-founder: something that gives Alfonso new perspectives and pushes back on his ideas using its own independently-built knowledge, not just a mirror of what he's already told it. It isn't scoped to a single business venture — it's scoped to Alfonso, continuously, across whatever ventures come and go.

## Core Value

A durable, cross-venture knowledge base that gives Alfonso a genuinely knowledgeable, independent thinking partner — without ever letting AI make strategic or creative decisions for him. Human judgment stays central to every strategic and creative call; that principle is non-negotiable and everything else in this project is built around protecting it.

## Scope

### In Scope

- Single local folder architecture: `raw/` (unprocessed sources, never edited), `wiki/` (Claude-organized, interlinked markdown — split into `shared/` and `claude-knowledge/`, paired by topic name and cross-linked), `index.md` (unified catalog across both wiki folders, folder-tagged per entry), `log.md` (append-only operation history)
- `CLAUDE-WIKI.md` at project root — the dedicated schema file governing ingestion workflow, query workflow, lint workflow, the new-page-vs-edit rule, the shared/claude-knowledge convention, and the propose-then-confirm rule for wiki writes
- `CLAUDE.md` kept thin — router only, pointing to where things live (wiki path, index, `CLAUDE-WIKI.md`, decision logs), not containing the operating rules itself
- `projects/` folder, one subfolder per venture, for venture-specific knowledge/discussion/decisions once a venture exists
- Three knowledge-growth mechanisms: (1) a deep research pass at ingestion of a new source — the one path that writes directly to the wiki without per-page confirmation, since handing over a source is already an act of trust; (2) manually-triggered periodic lint/health-checks that look for gaps, contradictions, stale claims, and missing cross-references, and can independently web-research to fill gaps; (3) an experience-feedback reconciliation loop, strictly propose-then-confirm, triggered when Alfonso reports real-world results from applying wiki knowledge
- The same propose-then-confirm pattern for filing ad-hoc conversational answers (a synthesized comparison or analysis that comes up in ordinary conversation) into the wiki
- "Grill me" — a standing interrogation tool/skill used for both initial knowledge extraction and reconciliation interrogation, adapted from existing proven skills (e.g. the `superpowers` repo) rather than built from scratch. **Status: landed as the `interrogate-me` skill** (`.claude/skills/interrogate-me/`) — in practice built as a custom design informed by researching several existing skills for technique inspiration, rather than adapted wholesale from one; see `.context/DECISIONS.md`'s 2026-07-21 entry.
- `About Me` — a file capturing what Claude learns about Alfonso, grown via the same grill-me process, included in lint passes but held to a lighter bar since it updates naturally through ordinary use
- Trust/verification tagging on wiki claims (extracted / inferred / ambiguous, per Graphify's convention) and a citation on every page (raw file, external research, or "synthesized from conversation on [date]")
- Index-first query discipline: read `index.md` first, drill into only relevant pages, never load the whole wiki into context
- Cross-venture learning by design — lessons from one venture are meant to inform another; the system tracks an evolving model of Alfonso, not a topic-indexed archive scoped to one business
- Local git version history (already initialized), no remote backup — worktrees/branches/PRs considered sufficient
- Obsidian as a visualization layer over the same file base — reverses the earlier deferral below once a felt need showed up (2026-07-21: wanting to browse via UI rather than VS Code folders). Vault config lives in `.obsidian/app.json` (gitignored, machine-local state); `.git/`, `.claude/`, `.agents/`, `.context/`, `node_modules/` are excluded from Obsidian's search and graph view so the graph stays focused on wiki content. No change to link syntax was needed — `CLAUDE-WIKI.md` §3.3's relative-markdown-links convention already renders correctly in Obsidian's graph view. See `.context/DECISIONS.md`.

### Explicitly Out of Scope

- Any automation on a timer — ingestion, lint, and reconciliation are all manually triggered, throughout this entire project, not just at launch
- Claude Code's built-in automemory feature — must be explicitly turned off; left on it would silently write to memory with no confirmation step, directly violating the propose-then-confirm principle the project is built around
- Vector search / embeddings infrastructure — not needed at current or near-term scale (up to roughly hundreds of pages); index-first reading substitutes for it
- Venture build-folders (an app's actual codebase, deployment config, etc.) living inside this repo — kept physically separate, driven by real risk (git history, build artifacts, secrets, CI/CD bleeding into a wiki folder). The exact connection mechanism between a venture's build folder and this second brain is a live, separate research thread and is not decided by this project
- A "hot cache" of recent conversational context — a real, precedented pattern from the source method, but not needed yet; worth revisiting only if reconstructing recent context from the wiki becomes expensive in practice

## Context

- Full conceptual grounding on the raw/wiki pattern and why it works was provided at initialization as `second-brain-general-concept.md` — a conversation input, not a file saved in this repo. It's background theory; its substance relevant to this project is already folded into this document.
- The project-specific design was decided through extended back-and-forth prior to this session and handed off as `build-handoff.md` — also a conversation input, not a repo file. It reflected real, already-made decisions (don't re-litigate what it settled), and everything from it that constrains future work has been captured in this OVERVIEW.md and in `.context/DECISIONS.md`. If a future session needs the original document, it no longer exists on disk — treat this OVERVIEW.md as the authoritative record of what it decided.
- **Core operating principle, stated explicitly and repeatedly in the handoff:** this is a direct lesson from a prior venture that failed specifically from over-delegating creative and strategic decisions to AI with minimal human oversight. Wherever Claude does something independently (research, drafting, proposing updates), assume it ends in a human checkpoint unless the deep-ingestion exception applies.
- Current state at initialization: two sources have been loosely ingested outside this formal system so far — Hormozi's *$100M Offers* and a negotiation book. These will likely need proper re-ingestion through Feature #1's actual workflow once it exists. No ventures are currently in flight.
- A separate, parallel effort is building a business-knowledge curriculum and source list. Its output will get ingested through the normal process once ready, but this build does not wait on it — the architecture is content-agnostic.
- Built using Alfonso's own `claude-workflow` tooling (installed at the user level, applies identically across this project and future venture builds): `/init-project` for this one-time setup, then the feature loop (`/feature` → `/feature-discuss` → `/feature-plan` → `/feature-execute` → `/feature-verify`, or `/feature-quick` for small well-understood work) for everything that gets built afterward.
- **Feature #1 must be the wiki structure itself** — `raw/`, `wiki/`, `index.md`, `log.md`, and `CLAUDE-WIKI.md`'s actual content — run through the full discuss/plan/execute/verify loop, not treated as boilerplate scaffolding. It's the single most deliberated part of the whole project (paired-folder convention, tagging system, propose-then-confirm, index-first design).
- **Superseded 2026-07-21 (see `.context/DECISIONS.md`):** the line below originally scoped ingestion/lint passes as future `/feature`-workflow items. That is no longer correct — the feature workflow governs building this project's own infrastructure only; ingestion, query, lint, and reconciliation are the second brain's ongoing operations and run directly per `CLAUDE-WIKI.md` §4–§9, with no feature ceremony. Kept below, struck through, for historical record of the original (mistaken) assumption: ~~a deep ingestion pass on a new source is a feature likely warranting full ceremony, given the research involved; a routine lint/health-check pass is a good fit for `/feature-quick`, being small, recurring, and well-understood.~~

## Constraints

- **Design**: `CLAUDE.md` stays thin — router only. It loads into every session's context automatically, so anything written directly into it is a fixed cost on every session whether or not that session needs it. Detailed operating rules belong in `CLAUDE-WIKI.md`, read only when a session is actually doing wiki work.
- **Process**: No automation on a timer anywhere in this project. Ingestion, lint, and experience-feedback reconciliation are all manually triggered, by design, throughout the project's life — not just deferred for launch.
- **Process**: Propose-then-confirm governs every wiki write except one named exception (the deep-ingestion pass on a brand-new source). This is the standing permission-layer principle for the whole system — filing ad-hoc conversational answers uses the same mechanism as the feedback loop, not a separate automatic path.
- **Tooling**: Claude Code's automemory feature must be explicitly disabled — this needs to be a deliberate, stated setting in `CLAUDE-WIKI.md`, not something left to default behavior.
- **Scope boundary**: Venture build-folders stay physically separate from this repo. The exact connection mechanism is an open, live research thread elsewhere and is not to be resolved by this build.

## Key Decisions

| Decision | Rationale |
|----------|-----------|
| Schema file is `CLAUDE-WIKI.md` at project root | Sibling to `CLAUDE.md`, keeps the router/detail split visible at a glance; decided live during this initialization rather than deferred to Feature #1 |
| `Claude-SecondBrain` (this repo) is the final home | Confirmed settled at initialization, though open to change later if a real reason emerges |
| Feature #1 = the wiki structure, run with full discuss/plan/execute/verify ceremony | The handoff treats this as the single most deliberated part of the whole project, not generic scaffolding an init script should default |
| Git initialized locally, no remote backup | Local version history plus worktrees/branches/PRs considered sufficient; not a designed artifact of the second brain itself, just standard project bookkeeping |

---
*Initialized: 2026-07-15*
