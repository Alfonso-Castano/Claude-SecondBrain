---
title: Ingestion, Growth, and Maintenance Mechanics
folder: shared
tags: [second-brain, ingestion, context-vs-connections, retrieval]
created: 2026-07-21
last_updated: 2026-07-21
source: raw/2026-07-21-second-brain-transcripts-full-summary.md
confidence: extracted
---

## You are in control of what gets ingested

Sources are not passively vacuumed in. A person actively decides to hand something over — "here's my meeting transcripts from this week, help me think through this and let's ingest it together." Ingestion is an act of deliberate curation, not an automatic sweep of everything that crosses a person's desk.

## Context vs. connections — a load-bearing distinction

The source material distinguishes two categories of data explicitly:

- **Context** — evergreen, still true and relevant a year from now, worth keeping permanently. This belongs in static files.
- **Connections** — fast-changing data (message threads, current customer/deal data). This kind of data should be *reachable* live rather than dumped into static files that immediately start going stale and require ongoing manual cleanup.

Getting this distinction wrong in either direction has a real cost: treating fast-changing data as if it were permanent context means the wiki silently accumulates stale claims nobody remembers to update; treating genuinely permanent background as if it needed a live connection adds unnecessary integration complexity for something that was never going to change.

## Layered lookup: how "connections" actually work in practice

A concrete illustration from the source material: a vague question like "what did we talk about with a specific person last week regarding a specific topic" gets answered by the agent checking a relevant **static file first**, then the **wiki**, and finally reaching into a **live connected tool** (a project-management platform, in the example given) only if the answer isn't found in the static layers.

This layered lookup, tried in the correct order, is itself what makes the system function as a genuine second brain rather than just a static archive. The static layers are cheap and fast to check; the live connection is the expensive fallback, reached only when the cheaper layers have already come up empty — not the first place the agent looks.
