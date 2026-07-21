# Decisions Log

Running record of decisions that constrain future work. Newest first. Any future session or skill should check here before re-deciding something already settled.

## 2026-07-21 — CLAUDE-WIKI.md schema-sync fixes from a file-base review pass

**Decision:** Following the first deep-ingestion pass (second-brain pattern knowledge), a review comparing the current file base (`CLAUDE-WIKI.md`, `ABOUT-ME.md`, the new wiki pages, and `interrogate-me`'s `references/`) against second-brain pattern research and Alfonso's own stated intent made three fixes directly to `CLAUDE-WIKI.md`: (1) §3.2 now requires every `paired_with` pairing to also have a real inline relative markdown link in the page body, not just the frontmatter field — Obsidian's graph view and backlinks don't render frontmatter as edges, so a pairing that exists only in `paired_with` is invisible when actually browsing the wiki; (2) the quick-reference table gained two previously-undocumented write paths: `ABOUT-ME.md` growth via `interrogate-me`, and a new "knowledge-testing companion file" write path that `interrogate-me`'s `references/knowledge-testing.md` introduced; (3) §2's minimum-bar rule (every page needs `confidence` + externally-bottoming `source`) gained an explicit exemption for knowledge-testing companion files, since they're diagnostic content about Alfonso's own grasp of a topic, not a claim about the world. Also fixed a stale claim in `ABOUT-ME.md` that said grill-me "doesn't exist yet."
**Rationale:** The schema was written before any real ingestion pass or the `interrogate-me` skill existed, so drift between the written rules and what actually got built was expected (see the 2026-07-17 "provisional, not settled" entry below) — this is exactly that drift surfacing and getting corrected on first contact with real content, not a sign of a design flaw.
**Made during:** Post-first-ingestion-pass review, alongside the deep-ingestion pass on second-brain pattern knowledge

## 2026-07-21 — RESOLVED: Feature #2 no longer waits on "grill me" — it exists

**Decision:** The 2026-07-17 open sequencing question (below) is resolved: `interrogate-me` (`.claude/skills/interrogate-me/`, with `references/about-me.md`, `references/ambiguous-resolution.md`, `references/knowledge-testing.md`) landed as a skill, built in a separate parallel session outside this project's feature workflow. The blocking condition named in the open question — "grill me" not existing yet — is satisfied. Business/domain knowledge re-ingestion (Hormozi's *$100M Offers*, the negotiation book) is unblocked and can proceed whenever it's next run, with `interrogate-me` available to resolve `ambiguous`-tagged content as `CLAUDE-WIKI.md` §4 and §9 assume.
**Rationale:** Directly resolves the condition the 2026-07-17 entry deliberately left open rather than defaulted. No interim ambiguous-content rule (option 2 in that entry) was needed since option 1's blocking condition cleared first.
**Made during:** Discovery that `interrogate-me` had landed (commits `24b2fb7`, `6e2b49e`), during the post-first-ingestion-pass review

## 2026-07-21 — Obsidian adoption reverses prior "explicitly out of scope" deferral

**Decision:** Obsidian is now installed (via `winget`) and configured as a visualization layer over the same file base, reversing `.context/OVERVIEW.md`'s original "Explicitly Out of Scope" status for it. Vault config lives in `.obsidian/app.json` (gitignored — machine-local state, not shared project state); `.git/`, `.claude/`, `.agents/`, `.context/`, `node_modules/` are excluded from Obsidian's search and graph view so the graph stays focused on wiki content. No change to `CLAUDE-WIKI.md` §3.3's relative-markdown-links convention was needed — confirmed Obsidian resolves standard markdown links for its graph view just as well as `[[wikilinks]]`, so migrating to wikilinks was considered and rejected.
**Rationale:** The original deferral was explicitly conditional — "until a specific pain point around visualizing relationships actually shows up" — not a permanent exclusion. That pain point showed up: Alfonso wants to browse the wiki via UI rather than VS Code folders. This is the deferred condition resolving as designed, not a scope-creep addition. Recorded here (and reflected in `.context/OVERVIEW.md`) because it reverses a documented Explicitly-Out-of-Scope line, which future sessions should not silently re-defer based on the stale original wording.
**Still open:** Whether to install the Obsidian Dataview plugin is undecided, pending Alfonso's call as part of a broader skills/plugins research pass.
**Made during:** Post-first-ingestion-pass review

## 2026-07-21 — Feature workflow scope clarified: infrastructure only, never second-brain operations

**Decision:** The `/feature-*` workflow (`/feature-discuss`, `/feature-plan`, `/feature-execute`, `/feature-quick`, `/feature-verify`) is scoped to building this project's own infrastructure and components — the kind of work Feature #1 (the wiki structure itself) was. It must never be used to wrap the second brain's ongoing knowledge operations — ingestion, query, lint, reconciliation — which are governed entirely by `CLAUDE-WIKI.md` §4–§9 and run directly in conversation, no feature ceremony. Stated explicitly in `CLAUDE-WIKI.md` §1 as a core operating principle, not left implicit.
**Rationale:** Alfonso caught this directly: a prior turn in this session conflated "ingest this document" with "should this go through the feature workflow," which is exactly the confusion this entry exists to prevent for future sessions. The feature workflow's job is building the second brain; it has no role in the second brain's own day-to-day functioning once built.
**Made during:** Discussion of the first real ingestion pass (second-brain methodology summary), post-Feature-#1-merge

## 2026-07-17 — ABOUT-ME.md vs. OVERVIEW.md split: confirmed deliberate, not an accidental gap

**Decision:** The split is intentional. `.context/OVERVIEW.md`'s Context section mentions Alfonso's prior venture failure (over-delegating creative/strategic decisions to AI) specifically because it is the direct causal justification for this project's propose-then-confirm principle — it is included as *project rationale*, scoped narrowly to "why this project's design is the way it is," not as a general biographical record. `ABOUT-ME.md` is the separate, deliberately broader personal model of Alfonso — his working style, preferences, other ventures, communication patterns, and anything else "grill me" surfaces over time — and stays empty until that process populates it. These are not duplicates of the same content at different addresses; they answer different questions ("why does this project have this constraint" vs. "who is Alfonso").
**Rationale:** Verified by re-reading both `CLAUDE-WIKI.md`/`ABOUT-ME.md` and `.context/OVERVIEW.md` directly rather than assuming. `OVERVIEW.md`'s own template/purpose (per `/init-project`'s conventions) is project context, not a person profile; the one biographical fact it contains is minimal-necessary, not a substitute for `ABOUT-ME.md`. Recording this explicitly because, before this entry, the split's rationale existed only as implicit design, not written down anywhere a future session would find it — a future session could plausibly have "cleaned up" the biographical mention out of `OVERVIEW.md` thinking it belonged only in `ABOUT-ME.md`, which would have deleted the project's own stated justification for its central design principle.
**Made during:** Post-merge review of Feature #1's file base against Alfonso's stated intent

## 2026-07-17 — Devil's-advocate design and several CLAUDE-WIKI.md mechanics are provisional, not settled

**Decision:** `CLAUDE-WIKI.md` §8's stakes-differentiated devil's-advocate design (independent non-communicating subagents for high-stakes pushback, inline for low-stakes) and several other mechanics — the citation-chain-bottoms-out-externally check (§6.2), earned-vs-mechanical `shared`/`claude-knowledge` pairing (§3.2), and the `index.md` size/rotation triggers (§6.2, and `log.md`'s own rotation trigger) — were all designed and locked into the schema before a single real ingestion or reconciliation pass has tested any of them against actual content. Nothing in `CLAUDE-WIKI.md` changes today as a result of this entry.
**Rationale:** These mechanics are well-reasoned (see `.context/research/SUMMARY.md` and the Feature #1 external review recorded above) but reasoning-from-first-principles is not the same as having survived contact with a real ingestion pass. Recording this now so they are revisited with real evidence once Feature #2 (or the first real reconciliation) actually exercises them, rather than being silently treated as permanently settled just because they are written down in a schema file. If Feature #2 or a later lint pass finds any of these mechanics don't hold up in practice, that is expected friction to resolve, not a sign the schema was built wrong.
**Made during:** Post-merge review of Feature #1's file base against Alfonso's stated intent

## 2026-07-17 — OPEN DECISION: does Feature #2 wait for "grill me," or does ingestion get an interim ambiguous-content rule?

**Decision:** Not resolved — deliberately left open for Alfonso, not picked silently.
**The problem:** `CLAUDE-WIKI.md` references the "grill me" interrogation skill as load-bearing in three places: resolving `ambiguous`-tagged content during ingestion (§4), the interrogation front-end for high-stakes reconciliation (§9), and as the only named mechanism for growing `ABOUT-ME.md`. None of this skill exists yet — it was explicitly deferred out of Feature #1's scope (see the 2026-07-15 "Research-surfaced gaps deferred to Feature #1" entry below, and `CONTEXT.md`'s Explicitly Out of Scope). Alfonso is building "grill me" in a separate, parallel chat right now.
**The two options, neither chosen here:**

1. **Feature #2 (re-ingesting the two held sources) waits** until "grill me" exists, so ingestion never hits an `ambiguous`-tagged point without the interrogation mechanism the schema assumes is there.
2. **`CLAUDE-WIKI.md` gets an explicit interim rule** for what happens when ingestion hits ambiguous content before "grill me" exists — e.g., tag it `ambiguous` per the existing trust-tag convention and leave it for a later "grill me" pass, rather than blocking the ingestion pass on something that doesn't exist yet.

**Why this is being surfaced, not resolved:** This is exactly the kind of sequencing call this project's own standing principle says should go to Alfonso, not be silently decided by whichever path a session happens to reach for. Whoever runs `/feature-discuss` for Feature #2 should raise this explicitly and get an actual answer before ingestion starts — not default to option 2 just because it's the path of least resistance.
**Made during:** Post-merge review of Feature #1's file base against Alfonso's stated intent

## 2026-07-17 — Depth preservation added as an explicit ingestion rule (CLAUDE-WIKI.md §4)

**Decision:** `CLAUDE-WIKI.md` §4 (ingestion workflow) now explicitly requires preserving a source's actual reasoning, nuance, caveats, and concrete examples rather than compressing into a tidy summary — stated as its own rule within point 2, and self-verification (point 4) now explicitly checks for lost depth as a distinct failure mode from faithfulness (a page can be accurate and still flattened).
**Rationale:** Alfonso has stated this directly and repeatedly as a real preference, and the original schema said nothing about depth vs. brevity — a real gap, since the default instinct under a structured ingestion workflow like this one is to compress. Checked directly against Karpathy's original "LLM Wiki" gist (`gist.github.com/karpathy/442a6bf555914893e9891c11519de94f`) before writing this: the source method itself is silent on depth-of-detail — it neither mandates nor discourages summarization. This confirms depth-preservation is Alfonso's own personalization layered on top of the pattern, not something to attribute to the reference method, and it's documented here with that provenance rather than overstated as source-grounded.
**Made during:** Post-merge review of Feature #1's file base against Alfonso's stated intent, fixed directly in `CLAUDE-WIKI.md` rather than deferred

## 2026-07-17 — Automemory-disable mechanism: confirmed and applied (supersedes 2026-07-15 entry)

**Decision:** Automemory is disabled for this repository via `autoMemoryEnabled: false` in the repo-local, committed `.claude/settings.json`. This is confirmed, not a lead: verified independently twice — once by Task 003 via the `update-config` skill (which found the key in Claude Code's own bundled settings schema, corroborating but independent of the earlier unverified subagent claim) and again during `/feature-verify`'s review pass (fetched Anthropic's live docs at `code.claude.com/docs/en/memory`, which state "set `autoMemoryEnabled` in your project settings"). Confirmed repo-scoped: `~/.claude/settings.json` (user level) contains no such key, so no other Claude Code project on this machine is affected.
**Rationale:** Automemory writing without confirmation directly violates this project's propose-then-confirm principle; the setting needed a verified (not guessed) mechanism before being relied on, per this project's standing caution around unverified subagent leads.
**Supersedes:** The 2026-07-15 "Automemory-disable mechanism: open item, needs verification" entry below — that entry's unverified lead is now confirmed correct and can be treated as resolved.
**Made during:** Feature #1 (Task 003, corroborated by `/feature-verify`)

## 2026-07-17 — Claude Code `@import` syntax confirmed: `@path`, no `import` keyword

**Decision:** Claude Code's file-import syntax for `CLAUDE.md` (and similar files) is `@path/to/file` — the `@` is immediately followed by the path, with no `import` keyword and no space (e.g. `@README`, `@ABOUT-ME.md`). Writing `@import ABOUT-ME.md` is invalid: the parser reads `@import` as an attempt to import a nonexistent file literally named `import`, leaving the intended path as inert trailing text that never actually loads.
**Rationale:** This exact mistake shipped in Feature #1's Task 006 (`CLAUDE.md` router) and was only caught by `/feature-verify`'s first pass (FAIL), fixed in Task 007, and independently re-confirmed against Anthropic's live docs (`code.claude.com/docs/en/memory`) in the re-review. Recording it here so future sessions writing or editing any `CLAUDE.md`-style import don't repeat it.
**Made during:** Feature #1 (Task 007 fix, confirmed in `/feature-verify` re-review)

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
