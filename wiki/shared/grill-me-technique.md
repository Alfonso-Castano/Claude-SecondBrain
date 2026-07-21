---
title: Grill Me — The Interrogation/Extraction Technique
folder: shared
tags: [second-brain, grill-me, knowledge-extraction, interrogation]
created: 2026-07-21
last_updated: 2026-07-21
source: raw/2026-07-21-second-brain-transcripts-full-summary.md
confidence: extracted
paired_with: ../claude-knowledge/knowledge-elicitation-interview-techniques.md
---

## What it is

A specific, named, reusable method: a skill that interviews a person relentlessly about a given topic — described examples in the source material range from roughly 15 to 30+ questions in a single session — continuing until the model judges it has extracted enough. It can also be fed supporting files (transcripts, contracts, documents) during the interrogation, not just verbal answers. Output is written into a dedicated "brainstorm" file/folder.

## What it's for

This is framed as a general-purpose knowledge-extraction tool, usable for:

- Initial business/personal background.
- A specific client or relationship.
- A specific business idea.
- As an entirely separate, later use: reconciling real-world feedback back into the wiki when something learned in practice diverges from what's currently written down.

## The underlying premise

The actual bottleneck in building a good second brain is often not "the AI isn't retrieving things well" — it's "not enough has actually been extracted out of the person's head and into the system yet." Before concluding retrieval is failing, the more useful question is whether the folders/files genuinely hold the full nuance a person actually has in their head, or whether there's simply a gap in what's been captured at all. A perfectly-indexed wiki of thin, under-extracted notes is not actually a working second brain — it just fails less visibly than one with obviously bad routing.

## Status in this project

Referenced in `CLAUDE-WIKI.md` as a load-bearing dependency in three places — resolving `ambiguous`-tagged content during ingestion, the interrogation front-end for high-stakes reconciliation, and the only named mechanism for growing `ABOUT-ME.md`. `CLAUDE-WIKI.md` and `.context/DECISIONS.md` (2026-07-17) both describe it as a future feature, deferred out of Feature #1's scope and being built in a separate, parallel session.

**Note as of this ingestion pass (2026-07-21): it has landed.** A skill named `interrogate-me` now exists at `.claude/skills/interrogate-me/SKILL.md` (with `references/about-me.md`, `references/ambiguous-resolution.md`, and `references/knowledge-testing.md`), present in this repo but not yet committed to git at the time of this pass. Its core technique — assess first without revealing anything (to avoid anchoring the person's answer on what they were just shown), treat free recall as a floor rather than a ceiling, then follow with structured cued questioning through the topic's actual sub-structure — matches the "grill me" pattern described in the source material closely, and its `references/` split (about-me, ambiguous-resolution, knowledge-testing) appears to map directly onto the three load-bearing uses `CLAUDE-WIKI.md` names for it. This page describes the general pattern from the source material; it does not describe `interrogate-me`'s actual implementation in detail, since that skill is its own artifact outside this ingestion pass's scope — but its existence is worth flagging directly to Alfonso, since it may resolve (or at least newly inform) the open sequencing question in `.context/DECISIONS.md`'s 2026-07-17 entry about whether Feature #2 should wait for this skill.

See [Knowledge Elicitation — Established Interview Technique](../claude-knowledge/knowledge-elicitation-interview-techniques.md) for the older, established discipline grill-me sits inside, and a concrete practice (a session-length cap) worth considering for `interrogate-me`.
