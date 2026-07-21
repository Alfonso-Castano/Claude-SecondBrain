---
title: Karpathy's LLM Wiki Method
folder: shared
tags: [second-brain, karpathy, llm-wiki, raw-wiki-pattern, level-2]
created: 2026-07-21
last_updated: 2026-07-21
source: raw/2026-07-21-second-brain-transcripts-full-summary.md
confidence: extracted
paired_with: ../claude-knowledge/karpathys-llm-wiki-method.md
---

## What this is

A specific, simple, non-technical method — originally described by Andrej Karpathy — for building a level-2 second brain (see the five-levels page) in a matter of minutes, requiring no fancy infrastructure. This is the concrete reference implementation this project's own `raw/`, `wiki/`, `index.md`, `log.md` structure is built on.

## The three-part structure

- **`raw/`** — unprocessed source material dropped in exactly as received (an article, a transcript, a PDF's contents, etc.), never edited by hand.
- **`wiki/`** — the organized output. The AI agent reads what's in `raw/` and organizes it into a set of interlinked markdown pages, deciding on its own how to chunk, structure, and cross-reference the material. The person does not need to pre-design a taxonomy or folder scheme.
- **`log`** — the operation history: a running record of what's been ingested and when.

Within `wiki/`, an **index** file catalogs everything — an entry per page, organized by category (tools, techniques, concepts, sources, people, comparisons, etc., depending on the project). The index is what an agent reads *first* when answering a question, before deciding which specific pages are actually worth opening in full. This index-first approach is what keeps token usage low even as the wiki grows.

**A router file (`CLAUDE.md` or equivalent) is still required** to explain how the project works: where the wiki path is, how to search through it, how to update it, and — per the guidance in the source material — explicit instruction on *when not to bother reading the wiki at all* for a given request, to avoid wasting tokens on lookups that aren't actually needed.

## Setup process (achievable in roughly 5 minutes)

1. Create a project folder.
2. Open an AI coding agent (Claude Code or equivalent) pointed at that folder.
3. Provide Karpathy's original idea/prompt (deliberately left vague/general by its author so it can be adapted per-project) directly to the agent, along with an instruction establishing it as "my LLM wiki agent — implement this as my second brain, guide me step by step, create the CLAUDE.md schema," etc.
4. The agent creates the initial folder structure. By default, it may create subfolders like `analysis/`, `concepts/`, `entities/`, and `sources/` — but this isn't fixed; the actual organizational scheme should be discussed and adjusted with the agent as real content starts populating it. Karpathy's own guidance is explicit that sometimes a flat structure with no subfolders at all is preferable, and other times subfolders genuinely help — there's no single correct answer; it depends on the nature of the content.
5. Drop a first real source into `raw/` and tell the agent to ingest it. The agent may ask clarifying questions first (what to emphasize, how granular to be, what the overall purpose of this specific vault/project is) — giving thorough answers to these upfront meaningfully shapes ingestion quality going forward. It helps to explicitly state the *purpose* of the whole project (e.g. "this is specifically for my second brain, for personal/business things" vs. "this is purely a research project") so future ingestion is contextually appropriate.
6. The agent reads the source and writes new wiki pages — potentially producing many pages from a single rich source (example given: roughly 25 wiki pages generated from one long article). This can take real time for large sources (example given: ~10 minutes for one long article; ~14 minutes to batch-ingest 36 video transcripts, producing 23 wiki pages).

## Obsidian's actual role

Obsidian is a free, optional tool that provides a *visual* layer (including a graph view) over the exact same underlying markdown files — it is not required infrastructure, and the system works identically without it. One source states he "hardly ever" opens Obsidian himself despite having it configured, specifically because he trusts that the underlying files and agent already handle retrieval correctly without needing the visual layer. If desired, a browser extension ("Obsidian Web Clipper") can pull web content directly into the `raw/` folder.

## "Hot cache"

A small, separate file (on the order of a few hundred words/characters) holding a compressed summary of the most recent relevant exchange or update — described specifically as useful in a *personal/business* second brain (where "what did we just discuss" recall matters), but explicitly **not** used in a more static, reference-style wiki (e.g. a video-transcript knowledge base), where that kind of "most recent thing" recall isn't a meaningful concept. This is a deliberate, contextual addition, not a universal requirement of the method — and per `.context/OVERVIEW.md`'s explicit scope, this project has deliberately not built one, revisiting only if reconstructing recent context from the wiki becomes expensive in practice.

## Linting / health checks

Karpathy's own described practice is to run periodic "LLM health checks" over the wiki — looking for inconsistent data, filling in missing data via independent web research, and identifying interesting new connections or candidate topics/articles worth adding. This is framed as routine maintenance, run as often as desired (daily, weekly, on-demand), not a one-time setup step.

## Does this replace semantic search / RAG?

The source material's own answer: "no, but kind of yes," depending on the project's actual scale and goals. Advantages of the raw/wiki approach over classic vector-based RAG:

- It finds information by reading indexes and following links, which preserves *relationship* meaning (rather than just similarity scores).
- Infrastructure cost is effectively zero beyond token usage — no embedding model, no vector database, no chunking pipeline to maintain.
- Maintenance is just periodic linting rather than needing to re-embed content whenever things change.

**The genuine limitation:** this approach doesn't scale to enterprise-level volumes (millions of documents) the way a dedicated vector/RAG pipeline does — at that scale, traditional retrieval infrastructure becomes necessary. At the scale of hundreds of pages (the range explicitly cited as where this method holds up well), the wiki approach is described as both cheaper and more accurate.

See [Karpathy's LLM Wiki Method — The Original Source, In Full](../claude-knowledge/karpathys-llm-wiki-method.md) for what going directly to the original gist adds beyond this summary — the Memex lineage, the `qmd` tool, and a real tradeoff this project's own ingestion design sits on one side of.
