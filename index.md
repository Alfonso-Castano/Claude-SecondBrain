# Index

Unified catalog of every page across `wiki/shared/` and `wiki/claude-knowledge/`, folder-tagged per entry. Read this first for any query — drill into individual pages only for what's relevant. Never load the whole wiki into context.

**Size trigger:** if this file exceeds ~150–200 entries or ~3–4k tokens, flag it during the next lint pass — that's the point at which index-first retrieval starts to strain.

---

## Second-brain pattern — core concepts

- [What a Second Brain Is](wiki/shared/second-brain-definition.md) — `shared` — Definition, the ephemeral-chat problem it solves, and the retrieval-first design mindset. Paired with claude-knowledge.
- [Second Brain — Landscape, Etymology, and Adjacent Paradigms](wiki/claude-knowledge/second-brain-definition.md) — `claude-knowledge` — Where "second brain" as a term comes from (Tiago Forte), and the digital-garden-vs-second-brain distinction (public vs. private).
- [The Four C's — Second Brain vs. AI Operating System](wiki/shared/four-c-model.md) — `shared` — Context/Connections/Capabilities/Cadence, in strict build order; why this project currently stops after the first two.
- [The Five Levels of Second Brain Maturity](wiki/shared/five-levels-of-second-brain-maturity.md) — `shared` — The full maturity ladder (exact-match router → LLM wiki → semantic search → knowledge graph → autonomous brain OS), diagnostic heuristics, and where this project sits (Level 2). Paired with claude-knowledge.
- [Context Rot — What the Research Actually Shows](wiki/claude-knowledge/context-rot-research.md) — `claude-knowledge` — Chroma's 2025 research study grounding the Level 5 "more context can hurt" concern with real data; includes a caveat to the "index-first retrieval makes more-is-better safe" claim.

## Karpathy's LLM Wiki method (this project's own architecture)

- [Karpathy's LLM Wiki Method](wiki/shared/karpathys-llm-wiki-method.md) — `shared` — The raw/wiki/index/log pattern, setup process, Obsidian's role, hot cache, linting. Paired with claude-knowledge.
- [Karpathy's LLM Wiki Method — The Original Source, In Full](wiki/claude-knowledge/karpathys-llm-wiki-method.md) — `claude-knowledge` — Direct read of the actual gist: the Memex lineage, the `qmd` tool, the log.md parseable-prefix trick, the one-at-a-time-vs-batch ingestion tradeoff, and explicit contradiction-flagging as part of the original pattern.
- [Ingestion, Growth, and Maintenance Mechanics](wiki/shared/ingestion-growth-maintenance-mechanics.md) — `shared` — Context-vs-connections distinction, layered lookup order for queries.
- [Real-World Second-Brain Implementations (Karpathy Pattern)](wiki/claude-knowledge/real-world-second-brain-implementations.md) — `claude-knowledge` — Comparison of public Claude-Code second-brain repos; surfaces a likely real gap in this project's schema (no ingestion-time contradiction-flagging).

## Grill me / knowledge extraction

- [Grill Me — The Interrogation/Extraction Technique](wiki/shared/grill-me-technique.md) — `shared` — What it is, what it's for, and its current status in this project (the `interrogate-me` skill has landed, see the page for detail). Paired with claude-knowledge.
- [Knowledge Elicitation — Established Interview Technique](wiki/claude-knowledge/knowledge-elicitation-interview-techniques.md) — `claude-knowledge` — The older knowledge-engineering discipline grill-me sits inside: structured vs. unstructured interviews, tacit knowledge, protocol analysis, and a concrete session-length best practice.

## Skills, delegation, and automation

- [Skills, Capabilities, and Delegation Patterns](wiki/shared/skills-and-delegation-patterns.md) — `shared` — Skills as permanently-unfinished artifacts, the assembly-line pattern, parallel delegation, CLI/API vs. MCP — and why this matches Alfonso's own multi-chat working style.
- [Cadence, Automation, and the Permission-Layer Principle](wiki/shared/automation-cadence-permission-layer.md) — `shared` — "A prompt is never a permission layer," the 150k-email incident, and why this is the load-bearing principle behind this project's entire design.

## AI thought-partner discipline

- [Using the AI as a Thought Partner — Usage Discipline](wiki/shared/ai-thought-partner-discipline.md) — `shared` — Sycophancy, the devil's-advocate sub-agent technique, self-verification, and citing sources — the direct grounding for `CLAUDE-WIKI.md` §8's pushback design.

## Comparative PKM methods and failure modes

- [Building a Second Brain (Tiago Forte) — CODE and PARA](wiki/claude-knowledge/building-a-second-brain-tiago-forte.md) — `claude-knowledge` — The mainstream "second brain" methodology; flags a direct tension between its progressive-summarization technique and this project's depth-preservation rule.
- [Zettelkasten and Atomic Notes — And a Correction to CLAUDE-WIKI.md](wiki/claude-knowledge/zettelkasten-atomic-notes.md) — `claude-knowledge` — Luhmann's method and atomic notes; corrects an overstated citation in `CLAUDE-WIKI.md` §3.2 about the literature-notes/permanent-notes distinction.
- [PKM Anti-Patterns and Failure Modes](wiki/claude-knowledge/pkm-anti-patterns-and-failure-modes.md) — `claude-knowledge` — Collector's fallacy, note rot, the twelve named anti-patterns, the "second brain delusion" — and which of `CLAUDE-WIKI.md`'s mechanisms do (and don't) defend against them.

---

*Last updated: 2026-07-21, first deep-ingestion pass (second-brain pattern knowledge).*
