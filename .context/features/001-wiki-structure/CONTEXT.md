# Feature: Wiki Structure

**Base:** a2db62c594f7d27a660b0a0773dceea9ebdbb67d

## Goal

Build the Second Brain's foundational structure and operating rulebook — folders, index/log files, the `CLAUDE.md` router, `ABOUT-ME.md`, and `CLAUDE-WIKI.md`'s full schema — so the first real ingestion pass (Feature #2) has a working system to write into.

## Scope

### In Scope

- Folders: `raw/`, `wiki/shared/`, `wiki/claude-knowledge/`, `projects/` (empty placeholder)
- `index.md` — seeded empty (header + "no pages yet"), not fake placeholder content
- `log.md` — seeded empty (header + format spec)
- `CLAUDE-WIKI.md` at project root — full schema: ingestion workflow (including the new self-verification step), query workflow, lint workflow (including proactive gap-surfacing), new-page-vs-edit rule, frontmatter template, anti-wikilink rule, earned-not-mechanical pairing rule, propose-then-confirm rule with the write-only-gating boundary stated explicitly, the devil's-advocate pushback design
- `CLAUDE.md` at project root — thin router (new file, doesn't exist yet)
- `ABOUT-ME.md` at project root — seeded placeholder; single-file-vs-folder form is an open question for the planner (see Open Questions)
- Automemory-disable task, executed via the `update-config` skill, verifying the real mechanism (supersedes the unverified lead recorded in `.context/DECISIONS.md` from initialization)
- Decision + likely adoption of markdown tooling (`package.json` + `markdownlint-cli2` + a link-checker) as real dev dependencies, pending a research pass confirming the specific tools

### Explicitly Out of Scope

- Building the "grill me" interrogation skill itself — deferred to its own future feature; `CLAUDE-WIKI.md` may reference it as a dependency without it existing yet
- Re-ingesting the two already-held sources ($100M Offers, negotiation book) — that's Feature #2, sequenced after this one
- Running an actual lint pass — nothing exists yet to lint
- A generic tool-agnostic mirror (e.g. `AGENTS.md`) — explicitly deferred, not dropped; revisit only if a different AI tool actually gets used (see `.context/DECISIONS.md`, 2026-07-17 entry)

## Implementation Decisions

- **Frontmatter schema** (Alfonso confirmed): every wiki page gets YAML frontmatter — `title`, `folder` (shared|claude-knowledge), `tags`, `created`, `last_updated`, `source`, `confidence` (extracted|inferred|ambiguous), `paired_with` (omitted if unpaired).
- **Markdown tooling** (Alfonso confirmed intent; specific tools flagged for research): `markdownlint-cli2` + a link-checker as real dev dependencies (`package.json`), run as the deterministic first step of every future lint pass — not a git hook, to avoid schedule-adjacent automation.
- **Pushback/devil's-advocate design** (Alfonso confirmed; strongly source-grounded per external review): pushback proposals present at least two named, genuinely-argued stances (case-for / case-against) instead of one verdict. High-stakes proposals (reconciliation overturning something, a trust-tag change, a contradiction) get the stances formed by **separate subagents** that don't see each other's conclusion while forming it. Low-stakes proposals (ad-hoc filing, minor additions) get this done inline by Claude, no subagents — avoids confirmation-fatigue ceremony on small things. Doubly source-grounded: the reference material's own thought-partner guidance (devil's advocate, multiple debating sub-agents) plus its independent sycophancy warning, converging with the automation-bias finding from this project's own research pass.
- **Propose-then-confirm gates writes only, never conversational pushback** (new, from external review — the sharpest catch in it): the devil's-advocate mechanism must fire immediately and un-gated in ordinary conversation. Only the actual wiki *write* waits on confirmation. `CLAUDE-WIKI.md` must state this boundary explicitly rather than leave it inferable, since confirm-gating quietly bleeding into conversational caution would work against the project's core principle.
- **Lint checklist** (expanded from original research per external review): `markdownlint-cli2` + link-checker pre-flight; orphan-page detection; index-entry-vs-page-content drift; citation-chain-bottoms-out-externally check (every `claude-knowledge` page's citation must trace outside the wiki, never to another wiki page); `index.md` size/token trigger (~150–200 entries or ~3–4k tokens); trust-tag enforcement in the query workflow (surfaced whenever a claim is cited back in conversation, not just when its page is opened); **plus proactively surfacing gaps and "interesting connections for new article candidates"** — lint isn't just hygiene, it's also meant to suggest what's worth researching or ingesting next.
- **Self-verification step in ingestion** (new, from external review): distinct from trust-tagging. Trust tags describe confidence; they don't substitute for Claude actually checking its own ingestion batch for accuracy before considering a deep-ingestion pass complete. Given deep ingestion writes directly with zero per-page human review, this is the pass's own closing step, not optional polish.
- **New-page-vs-edit rule**: default toward merge/edit over creating a new page, per Zettelkasten's atomic-note discipline — a new page only for something that's a genuinely distinct entity/concept worth linking to from elsewhere.
- **`shared`/`claude-knowledge` pairing is earned, not mechanical** (from original research): never create a stub on the other side of a pairing just to satisfy the convention — a known failure mode (low-information stub files diluting the index) in the closest analogous pattern (Zettelkasten literature-notes vs. permanent-notes).
- **Anti-wikilink rule**: standard relative markdown links (`[Topic](../claude-knowledge/topic.md)`) only, never `[[wikilink]]` syntax — no resolver exists for it since Obsidian is deferred.
- **`CLAUDE.md` router scope**: points to `.context/OVERVIEW.md`, `.context/STATE.md`, `CLAUDE-WIKI.md`, `.context/DECISIONS.md`, `index.md` (project root — per `OVERVIEW.md`, `index.md` and `log.md` are top-level components alongside `raw/` and `wiki/`, not nested inside `wiki/`). Also `@imports` `ABOUT-ME.md` directly (Claude's default judgment, not explicitly asked — About Me is meant to be read on most sessions per the external review's precedent, matching how `OVERVIEW.md`/`STATE.md` are already loaded via `@imports`; easily correctable if wrong).
- **`ABOUT-ME.md` at project root**, sibling to `CLAUDE.md`/`CLAUDE-WIKI.md` — reverses the earlier `wiki/shared/about-me.md` assumption. Source precedent: always-true, root-level context read on most sessions, structurally separate from the on-demand wiki. **Single file vs. a whole folder is unresolved** — see Open Questions.
- **`log.md` format** (Alfonso confirmed intent; exact format flagged for research): one line per operation, newest-first — `YYYY-MM-DD | <ingest|lint|reconcile|file> | <short description> | <files touched>`.
- **Automemory disable**: a task in this feature, using the `update-config` skill to verify the real disable mechanism and apply it scoped to this repo (see `.context/DECISIONS.md`, 2026-07-15 entry — the earlier subagent lead on `autoMemoryEnabled` is unverified and must not be hand-applied without confirmation).
- **`index.md`/`raw/`/wiki folders start genuinely empty** (Alfonso confirmed): no placeholder/example pages. First real content comes from Feature #2.
- **Tool-agnostic mirror**: explicitly deferred, not built now (Alfonso decided) — see Explicitly Out of Scope.

## Global Constraints

- `CLAUDE.md` stays thin — router/imports only, never inline operating rules. It loads into every session automatically; anything written directly into it is a fixed cost on every session.
- No automation on a timer, anywhere, ever, for any workflow (ingestion, lint, reconciliation) — always manually triggered, permanently, not just at launch.
- Propose-then-confirm governs every wiki *write* except the one named deep-ingestion exception — but never gates conversational pushback or disagreement, which must fire immediately and un-gated. This boundary must be explicit in `CLAUDE-WIKI.md`, not left implicit.
- Standard relative markdown links only, never `[[wikilink]]` syntax, anywhere in the wiki.
- Every wiki page requires frontmatter with, at minimum, a trust tag and a citation that bottoms out outside the wiki — no page without provenance.
- `shared`/`claude-knowledge` pairing is earned, never mechanical — do not create a stub on the other side of a pairing just to satisfy the convention.
- Human judgment stays central to every strategic/creative decision — the project's non-negotiable. If an implementation choice made during planning or execution seems to conflict with this, stop and flag it rather than resolve it silently.

## Open Questions

- **Exact markdown tooling**: `markdownlint-cli2` confirmed in spirit; which link-checker (`markdown-link-check` vs. `lychee`) and the `package.json` setup need a research pass — recommend `/feature-plan --thorough` (new dependency, not yet in the project's manifest).
- **`log.md` exact format**: the newest-first, pipe-delimited format proposed above is Alfonso-confirmed in intent but unvalidated against comparable implementations — include in the same research pass.
- **`ABOUT-ME.md`: single file vs. a whole folder** — genuinely unresolved; Alfonso wants root-level placement confirmed either way, but the folder-vs-file question needs research on whether a folder is a normal pattern in comparable second-brain implementations.
- **Exact `CLAUDE-WIKI.md` internal section structure/ordering** — left to the planner's judgment; the content requirements above are exhaustive, the document structure is not prescribed.
