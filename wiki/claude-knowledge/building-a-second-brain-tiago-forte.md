---
title: Building a Second Brain (Tiago Forte) — CODE and PARA
folder: claude-knowledge
tags: [second-brain, tiago-forte, para-method, code-method, progressive-summarization]
created: 2026-07-21
last_updated: 2026-07-21
source:
  - https://fortelabs.com/blog/basboverview/ (accessed 2026-07-21)
  - https://www.aftertone.io/productivity-guides/second-brain-para-method (accessed 2026-07-21)
  - https://readingraphics.com/book-summary-building-a-second-brain/ (accessed 2026-07-21)
confidence: inferred
---

## Why this page exists, and its confidence tag

This page reports Tiago Forte's actual methodology faithfully, which on its own would be `extracted`. But its real value to this project isn't the faithful report — it's a direct, concrete tension this method has with a rule already written into `CLAUDE-WIKI.md`, which is Claude's own connective observation rather than anything stated in the sources themselves. That's why this page is tagged `inferred`: the comparative judgment in the final section is the load-bearing content, not the summary above it.

## The premise

Building a Second Brain rests on the premise that the brain is better suited to *generating* ideas than *storing* them — the system exists to externalize storage so the brain can be freed up for synthesis and creative work, rather than acting as its own filing cabinet.

## The CODE method

Four steps, applied to a personal note-taking app (Forte's system is tool-agnostic in principle but is built around conventional note apps — Evernote, Notion, Obsidian — not an AI agent that writes the notes itself):

- **Capture** — anything and everything that catches your attention gets saved: ideas, quotes, articles, images.
- **Organize** — captured material gets sorted using PARA (below).
- **Distil** — each note gets progressively reduced to its essence via **progressive summarization** (see below).
- **Express** — the actual point of the whole system; everything before this step exists purely to enable it. Forte's framing treats Capture/Organize/Distil as scaffolding in service of eventually producing something, not as ends in themselves.

## Progressive summarization

This is Forte's specific technique for distilling a note across multiple encounters with it, rather than in one pass:

1. **First capture** — save the relevant passage as-is.
2. **First review** — bold the most interesting sentences.
3. **Second review** — highlight the most important bolded text (a subset of the bold).
4. **Subsequent engagement** — write a short summary at the top, in your own words.

Each pass compresses further. By the final layer, a reader skimming just the top-of-note summary gets the gist without reading the original passage at all — that's the explicit design goal, not an accidental side effect.

## PARA — organizing by actionability, not topic

- **Projects** — active, time-bound outcomes with a clear definition of done.
- **Areas** — ongoing responsibilities with no defined endpoint.
- **Resources** — topics of interest that may be useful in future.
- **Archives** — inactive items from any other category.

The design choice that most distinguishes PARA from conventional filing: information is organized by **actionability** — what it's *for*, right now — rather than by topic or subject matter. A note about "marketing" doesn't live in a "Marketing" folder; it lives wherever it's actually being used (a specific active Project, an ongoing Area of responsibility, or Resources if it's not yet in use).

## The direct tension with this project's own ingestion rule

**Progressive summarization is, by design, a compression technique.** Its entire mechanic is reducing a note's information density across successive passes until only the most essential fragment remains at the top layer — the opposite instinct from `CLAUDE-WIKI.md` §4's explicit depth-preservation rule, which requires the ingestion workflow to preserve a source's actual reasoning, nuance, caveats, and concrete examples rather than compressing it down to a tidy summary of conclusions.

This isn't a minor stylistic difference between two PKM methods — it's the most-cited, most mainstream "second brain" methodology in existence doing, as a named core technique, exactly the thing Alfonso explicitly told Claude not to do in this project. Two ways to read that:

- **In favor of Forte's approach:** progressive summarization is designed for a system a human personally re-reads and re-processes over time — the compression is earned through repeated human engagement with the material, not applied blindly on first ingestion. It optimizes for a human doing their own thinking work across multiple passes.
- **In favor of this project's depth-preservation rule:** this system's ingestion is a single AI-driven pass with zero per-page human review (the deep-ingestion exception to propose-then-confirm) — there is no equivalent "second review, third review" human loop happening here to progressively earn that compression. Applying Forte's compress-on-every-pass instinct to a single automated pass with no human re-engagement would just be lossy summarization with extra steps, which is precisely the failure mode `CLAUDE-WIKI.md` §4 was written to prevent.

Given this project's actual mechanics (single-pass, unsupervised, AI-authored), the depth-preservation rule is the better-fitted choice for *this specific system* — but that's a structural argument about how the two systems' human-involvement loops differ, not a claim that progressive summarization is a worse technique in general. Worth naming this precisely rather than either dismissing Forte's method or treating this project's own choice as beyond question.
