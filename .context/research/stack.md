# Stack Research: AI-Agent-Operated Markdown Knowledge Base

## Summary

This project is not inventing a new pattern — it's a direct implementation of what's now publicly known as "Karpathy's LLM Wiki" (raw/ → wiki/ → CLAUDE.md schema → index → lint), which went viral in April 2026 and already has an ecosystem of write-ups analyzing it. The base stack of "markdown files + git + Claude Code" is correct and sufficient; nothing more should be added as *infrastructure*. What's missing is a thin layer of **deterministic, non-AI tooling** (a markdown linter, a link checker, a frontmatter convention) that should run as a cheap pre-flight *inside* the already-planned manual lint pass — this doesn't violate the "no automation on a timer" rule because it's invoked by a human action, not a schedule, and it saves the AI's judgment budget for the semantic checks it's actually good at (contradictions, staleness, gaps).

## Findings

### 1. The base pattern is confirmed prior art, not a novel design

The project's raw/wiki/CLAUDE.md/index/lint structure matches the publicly documented "Karpathy method" closely: raw/ as immutable source, wiki/ as LLM-synthesized output, the schema file as governance ("the real product"), index.md as primary navigation up to roughly 100-200 pages, and lint as the health-check/self-repair function. **HIGH confidence** this is the right reference pattern to build from — it's not just one blogger's opinion, it's been independently written up by multiple outlets describing the same source material. One write-up explicitly frames the architecture as a compiler analogy: raw/ = source, LLM = compiler, wiki/ = build output, lint = tests, query = runtime — a useful mental model to carry into CLAUDE-WIKI.md's design. **MEDIUM confidence** on this specific framing (single-source, not cross-checked, but internally consistent with the rest).

One nuance worth flagging to the roadmapper: most public write-ups of this pattern recommend Obsidian as the front-end for humans browsing the wiki (graph view, backlinks) — this project has explicitly and deliberately deferred that. That's a legitimate divergence, not a gap; just confirms the OVERVIEW's framing that Obsidian is "a pure visualization layer," not a load-bearing part of the pattern itself.

### 2. Markdown link format: use standard relative links, not `[[wikilink]]` syntax — this is a real gap to flag

Public write-ups of this pattern (and PKM tools generally — Obsidian, Foam, Dendron) default to `[[Note Name]]` wikilink syntax for cross-references. **This is not standard CommonMark/GFM** — it only resolves visually or functionally in tools that implement a wikilink resolver (Obsidian, Foam, Dendron, some static site generators with a plugin). Since Obsidian is explicitly deferred and no resolver is planned, adopting `[[wikilinks]]` now would mean:
- Links render as literal broken text in plain GitHub/VS Code Markdown preview
- Any automated link-checking tool (see below) won't understand them without extra config
- If Obsidian is adopted later, migration is easy either way, so there's no real cost to waiting

**Recommendation (MEDIUM-HIGH confidence, inference from tool documentation cross-referenced with CommonMark spec):** use standard relative markdown links — `[Topic Name](../claude-knowledge/topic-name.md)` — for all wiki cross-references and index.md entries now. This is portable, git-diffable, greppable, and works with off-the-shelf link checkers with zero configuration. Revisit only if/when Obsidian is actually adopted. **This should be made an explicit rule in CLAUDE-WIKI.md** since Claude Code will otherwise plausibly default to `[[wikilink]]` syntax, having seen it constantly in PKM training data.

### 3. YAML frontmatter: adopt it now — it's the natural home for the trust-tagging and citation conventions already decided

The OVERVIEW already commits to trust/verification tags (extracted/inferred/ambiguous, per Graphify's convention — see Pitfalls/Architecture notes, not re-litigated here) and a citation on every page. YAML frontmatter (`---` delimited block at the top of a file) is the long-established, tool-agnostic convention for exactly this kind of page-level metadata — it predates and is independent of any specific static site generator (Jekyll popularized it, but it's now a de facto standard read natively or via trivial parsing by almost every markdown tool, including Claude Code itself). **HIGH confidence** this is standard and low-cost to adopt.

Concrete recommendation for CLAUDE-WIKI.md's page schema:
```yaml
---
title: <page title>
folder: shared | claude-knowledge
tags: [topic1, topic2]
created: 2026-07-15
last_updated: 2026-07-15
source: raw/<file> | external-research | conversation:2026-07-15
confidence: extracted | inferred | ambiguous   # or per-claim inline if mixed within a page
---
```
This gives every lint pass a cheap, deterministic thing to check (missing fields, stale `last_updated`, malformed `source`) before the AI has to reason about content semantics at all — a floor of structural correctness under the AI-driven judgment layer. One real pitfall observed in the wild: an agent generating `tags` as a comma-separated string instead of a YAML list produces technically-valid YAML that still breaks any tooling expecting a list — worth a one-line rule in CLAUDE-WIKI.md specifying the exact field types.

### 4. Deterministic markdown tooling worth adding as pre-flight to the lint pass (not new infrastructure — just scripts, no servers)

Two mature, widely-used, dependency-light CLI tools are relevant here and cost nothing beyond an npm/local install:

- **markdownlint-cli2** (or markdownlint-cli) — catches formatting drift: heading level skips, inconsistent list markers, trailing whitespace, malformed tables. **HIGH confidence**, actively maintained, the de facto standard markdown linter (also what most "awesome markdown" toolchains converge on). [github.com/DavidAnson/markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2)
- **A link checker** for catching genuinely broken cross-references and dead external URLs — either `markdown-link-check` (Node, JUnit-reporter support) or `lychee` (Rust, notably faster, handles local file links well). Given the project explicitly wants lint passes to catch "missing cross-references," this is a direct, cheap complement to the AI's semantic review — the AI shouldn't have to manually re-verify every link resolves; a deterministic tool should do that in milliseconds first. **HIGH confidence** these tools are standard for this purpose. [github.com/tcort/markdown-link-check](https://github.com/tcort/markdown-link-check), [github.com/lycheeverse/lychee-action](https://github.com/lycheeverse/lychee-action) (the Action wrapper is irrelevant here since there's no CI/remote, but the underlying `lychee` binary runs fine standalone/locally).

**Where these fit without violating "no automation on a timer":** run them as the *first, fast, non-AI step* of the manually-triggered lint pass — a human (or Claude, told to do so as step 1 of the lint workflow) runs the linter/link-checker locally, fixes or flags mechanical issues, and only then does Claude spend judgment on semantic lint (contradictions, staleness, gaps). This is action-triggered, not schedule-triggered, so it's consistent with the constraint as written. Do **not** wire these into a git pre-commit hook that fires automatically on every commit — that would be a form of always-on automation the project has deliberately ruled out for anything beyond version-control bookkeeping; keep it inside the manual lint invocation instead.

### 5. Established PKM philosophies (Zettelkasten, PARA) — deliberately don't import their structure, note only where they already overlap

Zettelkasten's core discipline (atomic, single-idea notes, densely cross-linked) and Karpathy's own guidance ("keep individual notes focused rather than combining multiple topics") point the same direction — this is worth stating explicitly as a page-granularity rule in CLAUDE-WIKI.md for Feature #1, since it affects when Claude should split a topic into two wiki pages vs. keep one. **MEDIUM confidence**, but low-risk, low-cost to adopt as a stated norm.

PARA (Projects/Areas/Resources/Archives) is a different paradigm — an actionability-based filing system for a single person's task-oriented notes — and doesn't map cleanly onto this project's `shared/` vs `claude-knowledge/` topic-paired convention or its `wiki/` vs `projects/` split. **Recommend not importing PARA's structure** — the project's existing scheme is already coherent and answers a different question (source of knowledge vs. actionability). Flagging this mainly so the roadmapper doesn't feel a gap here that needs filling; there isn't one.

### 6. Provenance beyond the citation footer: git itself is a free, already-present provenance layer — use it, don't duplicate it

Git already gives per-line blame and full commit history for every wiki page. This doesn't replace the explicit citation field (a git log entry doesn't tell a future reader *which raw source* a claim came from, only *when the file changed*), but it's a good complementary practice to establish now at near-zero cost: **write descriptive, structured commit messages when wiki pages are written/edited** (e.g., `ingest: <source> → <pages touched>`, `lint: fix N stale claims in <page>`, `reconcile: update <page> per experience feedback <date>`). This turns `git log` into a secondary, free audit trail that complements `log.md` rather than duplicating it — `log.md` is the human-readable narrative, git history is the mechanical diff-level record. **LOW-MEDIUM confidence** — general good-practice inference, not tied to a specific source, but low-risk and cheap to adopt as a convention in CLAUDE-WIKI.md.

### 7. What's genuinely *not* worth adding

- **A static site generator (Jekyll/Hugo/Docusaurus) or any publish step** — the project has no "read on the web" requirement; would add a build pipeline for no user. Don't add.
- **A git hook manager (`pre-commit` framework, Husky)** — solves the problem of *sharing* hooks across contributors/machines in a team repo; this is a single local repo with one human and one AI agent, so the coordination problem it solves doesn't exist here. Simple local scripts invoked manually as part of the lint workflow are sufficient and simpler to reason about (no framework config file to maintain). If Alfonso later works across multiple machines, revisit.
- **A wikilink resolver / Foam / Dendron VS Code extensions** — these are lightweight relative to Obsidian, but the OVERVIEW's Obsidian deferral is explicitly about not adding *any* visualization/navigation layer ahead of a felt need; these tools exist for the same job. Standard relative markdown links (point 2 above) already give 90% of the navigation benefit for free, with zero dependency.
- **`llms.txt`** (an emerging, not-yet-broadly-adopted convention for exposing an AI-readable doc index at a website's root) — conceptually similar in spirit to what `index.md` already does for this project, but it's a convention for *external* AI crawlers hitting a public website, not for a local agent with direct filesystem read access. Not applicable here; mentioning only so the roadmapper doesn't wonder if it was missed. **LOW confidence relevance** — noted for completeness, not a real gap.

## Confidence

**Overall: MEDIUM-HIGH.** The core architectural pattern (raw/wiki/index/lint) is HIGH confidence — well-documented, cross-checked across multiple independent write-ups of the same viral source material. The specific tooling recommendations (markdownlint-cli2, link checkers, YAML frontmatter) are HIGH confidence as *generically standard tools* but MEDIUM confidence in their specific fit to *this* project, since no source discusses this exact combination — that fit assessment is this researcher's inference, clearly labeled as such above.

## Sources

- [MindStudio — What Is the LLM Wiki? Karpathy's Knowledge Base Architecture for AI Agents](https://www.mindstudio.ai/blog/what-is-llm-wiki-karpathy-knowledge-base-architecture) — MEDIUM
- [MindStudio — What Is Andrej Karpathy's LLM Wiki? How to Build a Personal Knowledge Base With Claude Code](https://www.mindstudio.ai/blog/andrej-karpathy-llm-wiki-knowledge-base-claude-code) — MEDIUM
- [starmorph — How to Build Karpathy's LLM Wiki: The Complete Guide](https://blog.starmorph.com/blog/karpathy-llm-wiki-knowledge-base-guide) — MEDIUM
- [Agentic AI Foundation — Karpathy's LLM Wiki as Agent Memory](https://aaif.io/blog/karpathys-llm-wiki-as-agent-memory/) — MEDIUM
- [DAIR.AI Academy — LLM Knowledge Bases](https://academy.dair.ai/blog/llm-knowledge-bases-karpathy) — MEDIUM
- [Gist — LLM Wiki v2, extending Karpathy's pattern](https://gist.github.com/rohitg00/2067ab416f7bbe447c1977edaaa681e2) — MEDIUM
- [Augment Code — Graphify Ships v0.8.41: confidence tagging (EXTRACTED/INFERRED/AMBIGUOUS)](https://www.augmentcode.com/learn/graphify-knowledge-graph-skill-ai-coding-assistants) — MEDIUM (single source, confirms what OVERVIEW.md already cites)
- [markdownlint-cli2 (GitHub)](https://github.com/DavidAnson/markdownlint-cli2) — HIGH (official tool repo)
- [markdownlint-cli (GitHub)](https://github.com/igorshubovych/markdownlint-cli) — HIGH (official tool repo)
- [remark-lint (GitHub)](https://github.com/remarkjs/remark-lint) — HIGH (official tool repo)
- [markdown-link-check (GitHub)](https://github.com/tcort/markdown-link-check) — HIGH (official tool repo)
- [lychee-action / lychee (GitHub)](https://github.com/lycheeverse/lychee-action) — HIGH (official tool repo)
- [Foam (GitHub)](https://github.com/foambubble/foam) — HIGH (official repo, for context on wikilink-based tooling)
- [Dendron (GitHub)](https://github.com/dendronhq/dendron) — HIGH (official repo, for context on wikilink-based tooling)
- [pre-commit/pre-commit-hooks (GitHub)](https://github.com/pre-commit/pre-commit-hooks) — HIGH (official repo, cited to explain why it's *not* recommended here)
- [AGENTS.md](https://agents.md/) — HIGH (primary spec source, for context on CLAUDE.md's place in the broader convention landscape)
- [GitHub Docs — Using YAML frontmatter](https://docs.github.com/en/contributing/writing-for-github-docs/using-yaml-frontmatter) — HIGH (primary/official documentation source for the frontmatter convention)
