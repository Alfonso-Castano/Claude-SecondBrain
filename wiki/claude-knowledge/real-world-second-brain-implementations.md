---
title: Real-World Second-Brain Implementations (Karpathy Pattern)
folder: claude-knowledge
tags: [second-brain, implementations, comparison, contradiction-flagging, qmd]
created: 2026-07-21
last_updated: 2026-07-21
source:
  - https://github.com/NicholasSpisak/second-brain (accessed 2026-07-21)
  - https://github.com/jessepinkman9900/claude-second-brain (accessed 2026-07-21)
  - https://github.com/coleam00/second-brain-starter (accessed 2026-07-21)
confidence: extracted
---

## Why this page exists

Karpathy's gist went viral (17 million views within days of publication, per search results reviewed for this pass) and multiple people have since published their own working implementations as public repos. Comparing what they actually built — as opposed to just the abstract pattern — surfaces conventions that converged independently across implementations, and at least one real capability gap in this project's own schema. This is the "adapt existing, proven tools rather than build from scratch" principle from `raw/2026-07-21-second-brain-for-me.md` applied to schema design itself, not just to tooling choices.

## NicholasSpisak/second-brain

Structure:

```text
your-vault/
├── raw/                    # Inbox for source material
│   └── assets/             # Images and attachments
├── wiki/
│   ├── sources/             # Individual source summaries
│   ├── entities/             # People, organizations, products
│   ├── concepts/             # Theories, frameworks, ideas
│   ├── synthesis/             # Cross-source analyses
│   ├── index.md
│   └── log.md
├── output/                  # Generated reports
└── CLAUDE.md
```

Notable choices: a dedicated `synthesis/` subfolder specifically for cross-source analysis pages (distinct from single-source summaries), and an `output/` folder for generated reports that's separate from the wiki proper — treating "things produced in answer to a query" as different from "the wiki's own accumulated knowledge," which this project's own schema doesn't currently distinguish (an ad-hoc filed answer goes straight into the wiki per `CLAUDE-WIKI.md` §7.1, with no separate output staging area). Ships as an installable skill (`npx skills add NicholasSpisak/second-brain`) deployable across Claude Code, Cursor, Gemini CLI, and 40+ other platforms — a concrete instance of the tool-agnosticism principle actually implemented as distributable tooling, not just a design aspiration.

## jessepinkman9900/claude-second-brain

The most fully-featured of the implementations reviewed. Structure centralizes under `~/.claude-second-brain/`, supporting multiple independent "brains" (isolated git remotes, isolated search indexes) from one tool install. Five distinct page types, all with YAML frontmatter:

| Type | Path | Purpose |
| --- | --- | --- |
| `overview` | `wiki/overview.md` | "Evolving high-level synthesis" |
| `topic` | `wiki/[concept].md` | Concepts, domains, ideas |
| `entity` | `wiki/[name].md` | Persons, tools, companies, projects |
| `source-summary` | `wiki/sources/[slug].md` | One page per ingested source |
| `qa` | `wiki/qa/[slug].md` | Filed answers to notable queries |

Two points of direct, concrete relevance to this project's own schema:

**1. Explicit contradiction-flagging is a first-class ingestion step here**, not an afterthought: `/brain-ingest` "flags any contradictions with existing knowledge" as one of its named steps, and contradictions surface as `[!WARNING]` callouts directly inside page content, so a reader sees the conflict in place rather than having to discover it separately during a lint pass. **This project's `CLAUDE-WIKI.md` has no equivalent mechanism at ingestion time** — the closest thing is the lint pass's "index-entry-vs-page-content drift" and general staleness checks (§6.2), which are manually triggered and run later, not during ingestion itself. Given Karpathy's own gist explicitly names "noting where new data contradicts old claims" as part of the ingestion step itself (see [Karpathy's LLM Wiki Method — The Original Source, In Full](karpathys-llm-wiki-method.md)), this project's schema may be under-specified here relative to the source pattern it's implementing — worth flagging to Alfonso as a possible real gap, not just a stylistic difference between implementations.

**2. Hybrid hard framing against RAG:** this implementation states its own identity explicitly — "This is not a RAG system. It's not a chatbot over your notes. It's an actively maintained, cross-linked wiki" — while still using `qmd` (hybrid BM25/vector search) as a search *accelerant* layered on top of the wiki, not as a replacement retrieval mechanism. This is a concrete precedent for treating semantic search as an optional layer *added to* a level-2 wiki rather than a wholesale move to level 3 — relevant if this project's own vector-search question (currently deferred, see [The Five Levels of Second Brain Maturity](../shared/five-levels-of-second-brain-maturity.md)) ever gets revisited: the choice isn't binary between "stay at level 2" and "become level 3," there's a hybrid middle option other implementers have already validated in practice.

Other conventions worth noting: `/lint` explicitly checks for "orphan pages, broken links, unresolved contradictions, and data gaps" — closely matching this project's own §6.2 checks, suggesting that specific checklist has converged independently across implementations rather than being one person's idiosyncratic choice. `/brain-rebuild` is named explicitly as a *destructive* operation requiring approval before proceeding — a concrete precedent for how a propose-then-confirm gate gets implemented for a genuinely high-stakes structural operation, not just routine page edits.

## coleam00/second-brain-starter

A different flavor worth naming precisely rather than folding into the above: this one generates a personalized PRD for "a proactive, persistent AI assistant," pushing further into the Capabilities/Cadence side of the Four C's model (see that page) rather than staying at the Context/Connections knowledge layer this project is currently scoped to. Useful as a marker of how far this general pattern can be taken in practice — and, by contrast, a useful confirmation that this project's current scope (explicitly Context + Connections only, per `.context/OVERVIEW.md`) is a real, deliberate stopping point on a spectrum other implementers have kept going past, not an incomplete version of what "second brain" implementations are supposed to eventually become.

## What this comparison actually suggests for this project

Not a recommendation to adopt any of these wholesale — that would cut against "don't over-optimize before starting" — but two concrete, low-cost observations worth Alfonso's attention:

1. **The contradiction-flagging gap** is the one finding here with a plausible case for being an actual missing piece of `CLAUDE-WIKI.md` rather than just a different implementation's stylistic choice, since it's present both in Karpathy's own original description of the ingestion step and in at least one mature real-world implementation of the same pattern.
2. Everything else — separate `synthesis/`/`output/` folders, five formal page types, multi-brain support — is added complexity these implementations chose to take on, not complexity this project is missing by omission. Given this project's current scale (zero pages ingested before this pass) and Alfonso's own standing "begin using and fix what's needed" principle, none of it is recommended for adoption now.
