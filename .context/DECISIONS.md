# Decisions Log

Running record of decisions that constrain future work. Newest first. Any future session or skill should check here before re-deciding something already settled.

## 2026-07-17 — External second-brain review: corrections and additions to Feature #1

**Context:** During `/feature-discuss` for Feature #1, Alfonso got an independent review from a separate Claude chat that had ingested several second-brain source documents not available to this project directly. That review confirmed most of the design (raw/wiki/log.md structure, the deep-ingestion no-confirm exception, index-first retrieval, and — most importantly — the devil's-advocate pushback design, which it called the strongest source-match in the whole design, independently corroborated by the source material's own sycophancy warning) but surfaced several real corrections/additions:

- **Lint scope expands beyond hygiene.** In addition to broken links, orphaned pages, stale claims, and citation-chain checks, lint should proactively surface gaps and "interesting connections for new article candidates" — i.e. suggest what's worth researching or ingesting next, not just fix what already exists. This is a described capability in the source material, not an invented addition.
- **New ingestion step: self-verification, distinct from trust-tagging.** Trust tags (extracted/inferred/ambiguous) describe how confident a claim is; they don't substitute for Claude actually checking its own ingestion batch for accuracy before considering the pass complete. Given deep ingestion writes directly with zero per-page human review, this is a real gap — add an explicit "Claude verifies its own ingestion batch before the pass is considered finished" step to the ingestion workflow in `CLAUDE-WIKI.md`.
- **Propose-then-confirm gates writes only, never conversational pushback.** The sharpest catch in the review: if confirm-gating (which only exists to govern what gets *written* to the wiki) starts bleeding into how readily Claude voices disagreement in ordinary conversation — hedging or softening pushback because "writing requires confirmation" gets conflated with "disagreeing requires caution" — that works directly against this project's core principle rather than for it. `CLAUDE-WIKI.md` must state this boundary explicitly: the devil's-advocate mechanism fires immediately and un-gated in conversation; only the actual wiki write waits on confirmation.
- **About Me relocates out of the wiki.** Reverses the `/feature-discuss` Batch D assumption (`wiki/shared/about-me.md`). The source material has actual precedent: About Me lives as always-true, root-level context (alongside a decisions log), read on most sessions — structurally separate from the deep-knowledge wiki, which is read on demand. Alfonso wants an `ABOUT-ME.md` at project root, but whether it should be a single file or a whole folder is unresolved — **flagged for research during `/feature-plan --thorough`**, specifically checking whether a folder is a normal pattern in comparable second-brain implementations.
- **Tool-agnosticism artifact: explicitly deferred, not dropped.** The review noted that "tool-agnostic, just markdown files" was one of this project's own founding principles (`second-brain-general-concept.md`) but nothing in the current design actually implements it — `CLAUDE.md`/`CLAUDE-WIKI.md` are Claude-Code-specific entry points, with no generic mirror (e.g. an `AGENTS.md`) another AI tool could discover. **Decision: do not build this speculatively now.** The wiki content itself is plain markdown and already tool-readable; only the router-file naming is Claude-specific. Revisit only if a different tool actually gets used — consistent with the project's standing "don't add infrastructure before a felt need" rule.
- **Provenance accuracy confirmed, no fix needed:** `OVERVIEW.md` already correctly attributes trust-tagging to Graphify (not the second-brain source material) and already frames propose-then-confirm as Alfonso's own principle rather than something the reference pattern prescribes — the review was confirming these were already accurate, not catching drift.

**Made during:** `/feature-discuss` for Feature #1, after external review

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

## 2026-07-15 — Automemory-disable mechanism: open item, needs verification

**Decision:** Not yet decided. `build-handoff.md` requires Claude Code's built-in automemory feature be turned off for this project (it writes without confirmation, violating the propose-then-confirm principle). During initialization, an automemory instance was found actively writing session memory for this exact project at `~/.claude/projects/<project-id>/memory/`, outside this repo and untracked by the wiki's own log/citation/lint machinery.
A subagent lookup (claude-code-guide) reported that automemory is controlled by a project-scopable setting (`autoMemoryEnabled` in `.claude/settings.json`, with local/project settings taking precedence over the user-wide default) — meaning it could plausibly be disabled for this repo alone without affecting Alfonso's other Claude Code projects. **This claim is unverified** — the harness flagged the subagent's response as resembling injected instruction content, and neither the exact setting key nor the cited doc URLs were independently confirmed.
**Rationale for deferring:** No automemory content has actually been written from this session (verified — none was saved during this initialization). The fix should go through the `update-config` skill, which is built to configure `settings.json` correctly and can verify the real mechanism, rather than hand-applying an unverified JSON snippet.
**Next step:** Before or during Feature #1, use `update-config` to verify the actual disable mechanism and apply it scoped to this repo, then document the confirmed setting in `CLAUDE-WIKI.md`.
**Made during:** Project initialization

## 2026-07-15 — Pushback mechanism must present multiple debating perspectives, not one verdict

**Decision:** When Feature #1 designs the "Claude pushes back with independently-researched knowledge" mechanism (ingestion pushback, experience-feedback reconciliation, or any propose-then-confirm interaction), it must surface competing framings/stances that debate each other — not a single confident, well-researched verdict for Alfonso to simply accept or reject.
**Rationale:** Research run during initialization found that "I researched this independently" framing tends to *increase* human deference rather than provoke harder thinking (automation bias) — this would quietly undermine the project's core non-negotiable principle without the system ever technically breaking its own rules (see `.context/research/SUMMARY.md`, Pitfalls). Alfonso's review of that research identified a concrete, source-grounded countermeasure: the reference material's own guidance for using Claude as a thought partner is specifically to have Claude play devil's advocate and spin up multiple sub-agents/perspectives that actively debate each other, rather than deliver one synthesis. This is more concrete than the mitigation originally recorded in the research summary ("require Alfonso to articulate his own counter-reasoning") and supersedes it as the primary design requirement, not just one option among several.
**Applies to:** Feature #1's `/feature-discuss` for the reconciliation/pushback mechanism specifically — this is now a requirement to design against, not an abstract risk to keep in mind.
**Made during:** Context review, prior to Feature #1

## 2026-07-15 — Research-surfaced gaps deferred to Feature #1, not resolved here

**Decision:** Concrete gaps found during domain research (page-level YAML frontmatter template, anti-`[[wikilink]]` rule, earned-not-mechanical `shared`/`claude-knowledge` pairing, a concrete lint checklist, stakes-differentiated propose-then-confirm, reconciliation requiring Alfonso's own counter-reasoning rather than accept/reject) are recorded in `.context/research/SUMMARY.md` for Feature #1's discuss/plan loop to pick up, not decided or written into `CLAUDE-WIKI.md` during this initialization.
**Rationale:** Per the project's standing principle, decisions this substantive about the wiki's actual operating rules stay human-reviewed through the full feature loop rather than being defaulted by an init script.
**Made during:** Project initialization
