# Log

Append-only record of every wiki operation — ingestion, lint, reconciliation, and ad-hoc filing. Newest entry first (prepend, don't append to the bottom) so recent activity is visible without scrolling.

**Format:** one line per operation —
`YYYY-MM-DD | <ingest|lint|reconcile|file> | <short description> | <files touched>`

**Rotation trigger:** past ~500 entries, rotate this file to `log-YYYY.md` (starting a fresh `log.md`) and check for this during lint passes — mirrors `index.md`'s own size trigger.

---

2026-07-21 | reconcile | Full-repo review vs. general second-brain research: added §3.2 reciprocal-inline-link requirement for pairings, added §2 knowledge-testing exemption, added ABOUT-ME.md/knowledge-testing rows to the quick-reference table, fixed stale "grill-me doesn't exist yet" claim in ABOUT-ME.md, added reciprocal inline links to 3 pairs missing them | CLAUDE-WIKI.md, ABOUT-ME.md, wiki/shared/second-brain-definition.md, wiki/claude-knowledge/second-brain-definition.md, wiki/shared/karpathys-llm-wiki-method.md, wiki/shared/grill-me-technique.md, wiki/claude-knowledge/knowledge-elicitation-interview-techniques.md
2026-07-21 | ingest | Deep-ingestion pass: second-brain pattern knowledge (raw sources + independent research) — 9 shared pages, 8 claude-knowledge pages, 5 earned pairings | wiki/shared/second-brain-definition.md, wiki/shared/four-c-model.md, wiki/shared/five-levels-of-second-brain-maturity.md, wiki/shared/karpathys-llm-wiki-method.md, wiki/shared/ingestion-growth-maintenance-mechanics.md, wiki/shared/grill-me-technique.md, wiki/shared/skills-and-delegation-patterns.md, wiki/shared/automation-cadence-permission-layer.md, wiki/shared/ai-thought-partner-discipline.md, wiki/claude-knowledge/karpathys-llm-wiki-method.md, wiki/claude-knowledge/second-brain-definition.md, wiki/claude-knowledge/building-a-second-brain-tiago-forte.md, wiki/claude-knowledge/zettelkasten-atomic-notes.md, wiki/claude-knowledge/pkm-anti-patterns-and-failure-modes.md, wiki/claude-knowledge/real-world-second-brain-implementations.md, wiki/claude-knowledge/context-rot-research.md, wiki/claude-knowledge/knowledge-elicitation-interview-techniques.md, index.md
