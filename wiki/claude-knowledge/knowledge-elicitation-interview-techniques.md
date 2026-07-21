---
title: Knowledge Elicitation — Established Interview Technique
folder: claude-knowledge
tags: [second-brain, grill-me, knowledge-elicitation, interviewing, tacit-knowledge]
created: 2026-07-21
last_updated: 2026-07-21
source: https://www.numberanalytics.com/blog/ultimate-guide-knowledge-elicitation-expert-systems (accessed 2026-07-21)
confidence: extracted
paired_with: ../shared/grill-me-technique.md
---

## Why this page exists

"Grill me" (see the paired shared page) is a specific, named technique from the second-brain source material — but interviewing a person to extract knowledge they hold but haven't written down is a much older, established practice in its own right: **knowledge elicitation**, developed originally for building expert systems in classical AI, where the entire discipline exists because "the AI isn't retrieving things well" was so often actually "not enough was ever extracted from the expert's head in the first place" — the exact same diagnosis the second-brain source material makes about grill-me's purpose. This is directly actionable research, not background trivia: `interrogate-me`, the skill that has already landed in this repo implementing grill-me (see the shared page's status note), could plausibly benefit from these established practices if it hasn't already converged on them independently.

## The three-step process

Knowledge elicitation breaks into three stages: **elicitation** (getting the knowledge out), **analysis** (structuring what was said), and **structuring** (organizing it into a usable form) — a pipeline, not a single conversational pass. Grill-me's own two-step structure (assess, then extract — per `interrogate-me`'s `SKILL.md`) maps onto elicitation-then-structuring fairly directly, with analysis folded implicitly into the extraction step rather than being a separate distinguished phase.

## Structured vs. unstructured interviews

The most common elicitation technique is the interview, and it comes in two named modes:

- **Unstructured** — open and exploratory, no fixed questions prepared. Used to set the scene and gather contextual information at the *start* of the elicitation process, before the interviewer knows enough about the domain to ask good specific questions yet.
- **Structured** — a prepared, deliberate question set, used once the interviewer has enough grounding to know what specifically needs to be asked.

This maps closely onto `interrogate-me`'s own described sequencing: "assess first, reveal nothing" (open, unprompted recall — closer to unstructured) followed by "structured, cued follow-up: walk deliberately through the topic's actual sub-structure" once the free-recall pass has been exhausted. The knowledge-elicitation literature's version of this same insight is stated as its own established principle, independent of the second-brain source material: open interviewing surfaces what a person volunteers, but doesn't reliably surface everything they actually know, which is why it's treated as a first phase rather than the whole method — not a second-brain-specific insight, but a much older one from a different field arriving at the same structural answer.

## Other elicitation techniques beyond interviewing

The broader literature names several other techniques worth knowing exist, even if not directly relevant to grill-me's current design: **protocol analysis / think-aloud** (prompting the expert to verbalize their reasoning process while actually solving a problem, rather than describing it after the fact — captures reasoning that's hard to state declaratively), **task analysis**, **repertory grid analysis**, and **card sorting**. Think-aloud/protocol analysis in particular is a genuinely different mechanism from interviewing (capturing reasoning-in-action rather than reasoning-recalled) and could be a real, concrete extension worth considering for `interrogate-me` in domains where the thing being extracted is *how* Alfonso reasons through something, not just *what* he already believes about it — flagged as a possible idea, not a recommendation, since it wasn't asked for and evaluating it properly would need to go through `interrogate-me`'s own build process, not this ingestion pass.

## Tacit knowledge — the actual target

A recurring theme in this literature: interviewing experienced people specifically enables extraction of **tacit knowledge** — knowledge a person has and uses but has never had reason to articulate explicitly, precisely because it's never been asked for directly before. This is the same underlying premise the second-brain source material states about grill-me ("the actual bottleneck... is often... not enough has actually been extracted out of the person's head and into the system yet") — arrived at independently, in a completely different field, decades earlier. Two separate lines of reasoning converging on the same diagnosis is a stronger basis for taking the premise seriously than either alone.

## A concrete, practical constraint worth flagging

The knowledge-engineering literature gives a specific, actionable best practice not present anywhere in the second-brain source material: **sessions should be limited to a maximum of roughly 2 hours**, and — in domains where expertise changes over time — it's generally only worth eliciting the person's most recent 5-10 years of knowledge, since older knowledge risks being stale or superseded. The second-brain source material's own description of grill-me sessions (15 to 30+ questions) doesn't specify a time bound at all. Whether `interrogate-me` already has an implicit session-length discipline built in wasn't checked as part of this ingestion pass (that skill's actual implementation is out of scope here) — but this is a concrete, low-cost, independently-sourced practice worth surfacing to whoever maintains that skill, not just filed as trivia.

See [Grill Me — The Interrogation/Extraction Technique](../shared/grill-me-technique.md) for the second-brain-specific pattern this page grounds, and its current status in this project.
