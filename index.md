# Index

Unified catalog of every page across `wiki/shared/` and `wiki/claude-knowledge/`, folder-tagged per entry. Read this first for any query — drill into individual pages only for what's relevant. Never load the whole wiki into context.

**Size trigger:** if this file exceeds ~150–200 entries or ~3–4k tokens, flag it during the next lint pass — that's the point at which index-first retrieval starts to strain.

---

## Second-brain pattern — core concepts

- [What a Second Brain Is](wiki/shared/second-brain-definition.md) — `shared` — Definition, the ephemeral-chat problem it solves, and the retrieval-first design mindset. Paired with claude-knowledge.
- [Second Brain — Landscape, Etymology, and Adjacent Paradigms](wiki/claude-knowledge/second-brain-definition.md) — `claude-knowledge` — Where "second brain" as a term comes from (Tiago Forte), and the digital-garden-vs-second-brain distinction (public vs. private).
- [The Four C's — Second Brain vs. AI Operating System](wiki/claude-knowledge/four-c-model.md) — `claude-knowledge` — Context/Connections/Capabilities/Cadence, in strict build order; why this project currently stops after the first two. Reclassified from `shared` — no demonstrated engagement with this specific framework found on review (§3.2's mastery bar).
- [The Five Levels of Second Brain Maturity](wiki/shared/five-levels-of-second-brain-maturity.md) — `shared` — The full maturity ladder (exact-match router → LLM wiki → semantic search → knowledge graph → autonomous brain OS), diagnostic heuristics, and where this project sits (Level 2). Paired with claude-knowledge.
- [Context Rot — What the Research Actually Shows](wiki/claude-knowledge/context-rot-research.md) — `claude-knowledge` — Chroma's 2025 research study grounding the Level 5 "more context can hurt" concern with real data; includes a caveat to the "index-first retrieval makes more-is-better safe" claim.

## Karpathy's LLM Wiki method (this project's own architecture)

- [Karpathy's LLM Wiki Method](wiki/shared/karpathys-llm-wiki-method.md) — `shared` — The raw/wiki/index/log pattern, setup process, Obsidian's role, hot cache, linting. Paired with claude-knowledge.
- [Karpathy's LLM Wiki Method — The Original Source, In Full](wiki/claude-knowledge/karpathys-llm-wiki-method.md) — `claude-knowledge` — Direct read of the actual gist: the Memex lineage, the `qmd` tool, the log.md parseable-prefix trick, the one-at-a-time-vs-batch ingestion tradeoff, and explicit contradiction-flagging as part of the original pattern.
- [Ingestion, Growth, and Maintenance Mechanics](wiki/shared/ingestion-growth-maintenance-mechanics.md) — `shared` — Context-vs-connections distinction, layered lookup order for queries.
- [Real-World Second-Brain Implementations (Karpathy Pattern)](wiki/claude-knowledge/real-world-second-brain-implementations.md) — `claude-knowledge` — Comparison of public Claude-Code second-brain repos; surfaces a likely real gap in this project's schema (no ingestion-time contradiction-flagging).

## Interrogation & knowledge extraction (grill-me / interrogate-me)

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

## Business — offers, pricing, and value (Hormozi, $100M Offers)

The seven `claude-knowledge` pages below were reclassified from `shared` on 2026-07-23 per
`CLAUDE-WIKI.md` §3.2 (verified mastery, not provenance). An `interrogate-me` pass on
2026-07-24 then verified Alfonso's own grasp of five of the seven sub-topics (thinner,
partial versions in his own framing — see each `shared` page for exactly what's verified
vs. still a gap), producing `shared` companions for those five. Two — the offer-construction
process and the naming formula — stayed `claude-knowledge`-only; his grasp of those wasn't
verified this pass. See the [knowledge check](wiki/shared/100m-offers-knowledge-check.md)
for the full per-sub-topic breakdown of what's solid vs. shaky.

- [The Grand Slam Offer Framework — Alfonso's Understanding](wiki/shared/grand-slam-offer-framework.md) — `shared` — Core tagline and price-vs-value distinction, verified; the "category of one" mechanism, not yet. Paired with claude-knowledge.
- [The Grand Slam Offer Framework (Hormozi)](wiki/claude-knowledge/grand-slam-offer-framework.md) — `claude-knowledge` — Core definition, commoditization vs. differentiation, the 22.4x money-math example, the acquisition.com business model, and Hormozi's origin story.
- [Finding a Starving Market — Alfonso's Understanding](wiki/shared/finding-a-starving-market.md) — `shared` — Thin: niching-down is solid, the four-indicator framework is not. Paired with claude-knowledge.
- [Finding a Starving Market (Hormozi)](wiki/claude-knowledge/finding-a-starving-market.md) — `claude-knowledge` — The four market indicators (pain, purchasing power, targetability, growth), the Lloyd/newspapers cautionary tale, market > offer > persuasion ordering, niching down and the Dan Kennedy pricing example.
- [Premium Pricing and the Virtuous Cycle of Price — Alfonso's Understanding](wiki/shared/premium-pricing-virtuous-cycle.md) — `shared` — The causal mechanism, reconstructed via his own reasoning; terminology and case study not yet verified. Paired with claude-knowledge.
- [Premium Pricing and the Virtuous Cycle of Price (Hormozi)](wiki/claude-knowledge/premium-pricing-virtuous-cycle.md) — `claude-knowledge` — Why raising price usually beats lowering it, the virtuous/vicious pricing cycle, the wine-tasting study, and the Gym Launch premium-pricing case study.
- [The Value Equation — Alfonso's Understanding](wiki/shared/value-equation-hormozi.md) — `shared` — Weak unprompted recall, strong applied use of 3 of 4 drivers on a novel case. Paired with claude-knowledge.
- [The Value Equation (Hormozi)](wiki/claude-knowledge/value-equation-hormozi.md) — `claude-knowledge` — The four value drivers (dream outcome, likelihood of achievement, time delay, effort/sacrifice), psychological vs. logical solutions, and the meditation-vs-Xanax worked comparison.
- [Constructing a Grand Slam Offer — The Five-Step Process (Hormozi)](wiki/claude-knowledge/constructing-a-grand-slam-offer.md) — `claude-knowledge` — Divergent thinking, dream outcome → problems → solutions → delivery vehicles → trim and stack, and the sales-to-fulfillment continuum. No `shared` companion — weakest sub-topic in the 2026-07-24 interrogation.
- [Enhancing Offers — Scarcity, Urgency, Bonuses, and Guarantees — Alfonso's Understanding](wiki/shared/enhancing-offers-scarcity-urgency-bonuses-guarantees.md) — `shared` — His strongest chapter — guarantees, scarcity/urgency, and bonuses all solid, with named specific gaps. Paired with claude-knowledge.
- [Enhancing Offers — Scarcity, Urgency, Bonuses, and Guarantees (Hormozi)](wiki/claude-knowledge/enhancing-offers-scarcity-urgency-bonuses-guarantees.md) — `claude-knowledge` — The delicate dance of desire, scarcity/urgency tactics, bonus-stacking rules, and the four types of guarantees.
- [Naming Offers — The MAGIC Formula (Hormozi)](wiki/claude-knowledge/naming-offers-magic-formula.md) — `claude-knowledge` — The Magnetic-reason/Avatar/Goal/Interval/Container naming formula and the offer-fatigue escalation sequence. No `shared` companion — near-total gap in the 2026-07-24 interrogation.
- [Knowledge Check — $100M Offers](wiki/shared/100m-offers-knowledge-check.md) — `shared` — Per-sub-topic diagnostic of Alfonso's actual grasp of the whole book; exempt from the trust-tag/citation requirement (diagnostic, not a claim about the world).

---

*Last updated: 2026-07-23, reclassification of Hormozi and Four C's pages from `shared` to `claude-knowledge` per `CLAUDE-WIKI.md` §3.2's redefinition.*
