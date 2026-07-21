---
title: Karpathy's LLM Wiki Method — The Original Source, In Full
folder: claude-knowledge
tags: [second-brain, karpathy, llm-wiki, primary-source, memex]
created: 2026-07-21
last_updated: 2026-07-21
source: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f (accessed 2026-07-21)
confidence: extracted
paired_with: ../shared/karpathys-llm-wiki-method.md
---

## Why this page exists

The paired [Karpathy's LLM Wiki Method](../shared/karpathys-llm-wiki-method.md) page is faithful to what the raw transcript summary reported about Karpathy's method. This page goes back to Karpathy's actual gist directly — fetched and read in full for this ingestion pass — because it contains real, substantive material the transcript summary didn't carry: a different core framing (compilation vs. retrieval), a named intellectual lineage (Vannevar Bush's Memex), a concrete CLI tool recommendation, a practical `log.md` formatting trick, and an explicit statement of the ingestion cadence tradeoff (one-at-a-time vs. batch) that this project's own deep-ingestion pass sits on one side of. This is not a restatement of the shared page — it's what going to the primary source actually adds.

## The core framing: compilation, not retrieval

Karpathy's own framing is sharper than "wiki vs. RAG" — he frames it as a category difference in what happens to knowledge over time:

> "Most people's experience with LLMs and documents looks like RAG: you upload a collection of files, the LLM retrieves relevant chunks at query time, and generates an answer. This works, but the LLM is rediscovering knowledge from scratch on every question. There's no accumulation."

Against this, the wiki pattern: "the LLM doesn't just index it for later retrieval. It reads it, extracts the key information, and integrates it into the existing wiki — updating entity pages, revising topic summaries, noting where new data contradicts old claims, strengthening or challenging the evolving synthesis. The knowledge is compiled once and then *kept current*, not re-derived on every query."

The metaphor he reaches for explicitly: **"Your PDFs and notes are the source code. The wiki is the binary."** And the full workflow metaphor he uses for his own actual practice: "the LLM agent open on one side and Obsidian open on the other... Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

## Contradiction-handling is explicit in the original pattern

Worth flagging directly: Karpathy's own description of ingestion explicitly includes **"noting where new data contradicts old claims, strengthening or challenging the evolving synthesis"** as part of what the LLM does on every ingest — this is not an optional extra some implementations bolted on later. It is part of the core pattern from the source itself. (See [Real-World Second-Brain Implementations](real-world-second-brain-implementations.md) for how several real implementations turned this into an explicit `[!WARNING]`-callout mechanic — and note that this project's own `CLAUDE-WIKI.md` does not currently have an explicit contradiction-flagging step, only the lint-pass's "stale claims" check, which fires later and only on manual trigger rather than at ingestion time.)

## The three layers, as Karpathy names them

- **Raw sources** — the curated, immutable collection. The LLM reads from it but never modifies it. Source of truth.
- **The wiki** — LLM-owned entirely. Summaries, entity pages, concept pages, comparisons, an overview, a synthesis. "You read it; the LLM writes it."
- **The schema** — the router document (`CLAUDE.md` / `AGENTS.md`) that tells the LLM the wiki's structure, conventions, and workflows. Karpathy's own description: "it's what makes the LLM a disciplined wiki maintainer rather than a generic chatbot. You and the LLM co-evolve this over time as you figure out what works for your domain." — i.e. the schema file is explicitly meant to be a living document that changes as real use reveals what works, not a one-time specification. This matches `.context/DECISIONS.md`'s framing of several `CLAUDE-WIKI.md` mechanics as "provisional, not settled" — that provisionality is the pattern working as intended, not a gap in this project's design.

## Ingestion cadence: Karpathy prefers one-at-a-time, with a real tradeoff named

"A single source might touch 10-15 wiki pages. Personally I prefer to ingest sources one at a time and stay involved — I read the summaries, check the updates, and guide the LLM on what to emphasize. But you could also batch-ingest many sources at once with less supervision. It's up to you to develop the workflow that fits your style."

This is directly relevant to how this project's own deep-ingestion pass is designed: `CLAUDE-WIKI.md` §4 explicitly chose the **batch, no-per-page-confirmation** side of this named tradeoff, on the reasoning that handing over a source is itself an act of trust. Karpathy's own stated personal preference is the opposite — the more supervised, one-at-a-time mode. Neither is "the" correct choice per the source material; Karpathy frames it as a style choice each person has to make, not a settled best practice. Worth knowing this project's choice is a deliberate departure from the pattern's own author's personal habit, not an oversight.

## Query: good answers get filed back in

"Answers can take different forms depending on the question — a markdown page, a comparison table, a slide deck (Marp), a chart (matplotlib), a canvas. The important insight: good answers can be filed back into the wiki as new pages. A comparison you asked for, an analysis, a connection you discovered — these are valuable and shouldn't disappear into chat history." This is the direct source-grounding for `CLAUDE-WIKI.md`'s "file an ad-hoc answer into the wiki" write path (propose-then-confirm gated, per §7).

## index.md and log.md: distinct purposes, stated precisely

Karpathy is precise about the difference: **`index.md` is content-oriented** (a catalog, organized by category, read first on every query to identify which pages are worth opening). **`log.md` is chronological** (append-only, what happened and when).

A concrete, practical tip from the source not present in the transcript summary at all: **if every log entry starts with a consistent prefix** (his example: `## [2026-04-02] ingest | Article Title`), the log becomes parseable with plain Unix tools — `grep "^## \[" log.md | tail -5` gives the last 5 entries without needing the LLM to read and reason over the whole file. This project's own `log.md` uses a different but structurally similar convention (`YYYY-MM-DD | <type> | <description> | <files>`), which is equally grep-able — worth confirming this was a deliberate design choice for that reason, since the file's own header doesn't currently state the rationale.

## The optional CLI-tooling layer: qmd

At scale beyond what the index file alone comfortably handles, Karpathy names a specific tool: **[`qmd`](https://github.com/tobi/qmd)** — a local search engine for markdown files with hybrid BM25/vector search and LLM re-ranking, running entirely on-device, with both a CLI (so the agent can shell out to it) and an MCP server (so the agent can use it as a native tool). Several real-world implementations of this pattern (see [Real-World Second-Brain Implementations](real-world-second-brain-implementations.md)) have already adopted `qmd` as their level-3-equivalent search layer. This project has not — consistent with `.context/OVERVIEW.md`'s explicit scope decision that vector/semantic search infrastructure isn't needed at current or near-term scale (see [The Five Levels of Second Brain Maturity](../shared/five-levels-of-second-brain-maturity.md)).

## The Memex lineage

Karpathy explicitly traces the idea's intellectual ancestry: "The idea is related in spirit to Vannevar Bush's Memex (1945) — a personal, curated knowledge store with associative trails between documents. Bush's vision was closer to this than to what the web became: private, actively curated, with the connections between documents as valuable as the documents themselves. **The part he couldn't solve was who does the maintenance. The LLM handles that.**" This is a striking, specific claim worth preserving rather than compressing: the argument isn't just "wikis are useful," it's that this pattern solves an 80-year-old, previously-unsolved problem in Bush's own original vision — the maintenance-labor bottleneck — and that solving *that specific bottleneck* is the actual novelty, not the markdown-files-and-folders mechanics themselves.

## Why the method works, in Karpathy's own words

"The tedious part of maintaining a knowledge base is not the reading or the thinking — it's the bookkeeping. Updating cross-references, keeping summaries current, noting when new data contradicts old claims, maintaining consistency across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. The wiki stays maintained because the cost of maintenance is near zero. The human's job is to curate sources, direct the analysis, ask good questions, and think about what it all means. The LLM's job is everything else."

## The document's own stated scope

Karpathy is explicit that the gist is deliberately abstract and incomplete by design: "This document is intentionally abstract. It describes the idea, not a specific implementation... Everything mentioned above is optional and modular — pick what's useful, ignore what isn't... The right way to use this is to share it with your LLM agent and work together to instantiate a version that fits your needs. The document's only job is to communicate the pattern. Your LLM can figure out the rest." This directly confirms (independently of the reasoning already in `.context/DECISIONS.md`'s 2026-07-17 entry on depth-preservation) that the source pattern itself is genuinely silent on implementation specifics like depth-vs-brevity, folder taxonomy, and page-type schemas — this project's specific choices on all of those axes are its own design decisions layered on top of the pattern, not something attributable to Karpathy's original idea.
