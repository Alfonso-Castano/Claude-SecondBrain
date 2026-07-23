---
name: ingest-source
description: Runs a deep-ingestion pass — reading a source file in raw/ and writing its content into the wiki (wiki/shared/ or wiki/claude-knowledge/) as properly-structured, trust-tagged pages, per CLAUDE-WIKI.md §4. Use when the user asks to ingest a source, points at a file they just dropped in raw/, or says something like "ingest this," "add this to the wiki," "run the ingestion skill on X." Not for interrogate-me sessions, ad-hoc conversational answers, or /feature-* work — this is specifically for taking a raw source and turning it into wiki pages.
---

# Ingest Source

## What this skill does

Formalizes deep ingestion (`CLAUDE-WIKI.md` §4) into a repeatable, invokable procedure, so
the read-order, chunking approach, and self-verification requirement don't have to be
hand-reconstructed from scratch every time a fresh session runs one. It does not change
`CLAUDE-WIKI.md` §4's actual organizing logic — that stays authoritative. This skill is the
consistent front door to it.

## How it's invoked

The user drops a source file in `raw/`, then runs this skill with the file's path, and
optionally a summary of what to emphasize:

```
/ingest-source raw/2026-07-22-100m-offers-hormozi-audiobook-transcript.md
/ingest-source raw/2026-07-30-some-youtube-transcript.md "Pay special attention to the
part around minute 20 where he describes his pricing test — I think that's the most
important part of this video."
```

If no summary is given, ingest broadly and generally — don't require one.

## Before starting

Read, in this order:

1. `CLAUDE.md` (router).
2. `CLAUDE-WIKI.md` in full — §2 (frontmatter template), §3 (page structure rules,
   including the `shared`/`claude-knowledge` definition), and §4 (the ingestion workflow
   itself) all apply directly to this pass.
3. `index.md` — so you know what's already in the wiki and don't duplicate it.
4. Do not use any `/feature-*` command or workflow. Ingestion is a second-brain operation,
   not project-infrastructure work (`CLAUDE-WIKI.md` §1's first bullet).

## Identify the source type, then read the matching reference file

Check `references/` (next to this file) for the file matching what kind of source this is,
and read it before segmenting — each one covers what's actually different about how that
kind of source is structured and what to watch for when turning it into wiki pages:

- **`references/written-text-ingestion.md`** — books, articles, and written/text-based
  course material. Anything where the source is prose someone wrote.
- **`references/spoken-transcript-ingestion.md`** — YouTube/video transcripts, podcasts,
  and spoken/recorded course lectures. Anything where the source is a transcript of someone
  speaking.

These two cover the two shapes source material actually comes in — written or spoken —
regardless of the specific label (book vs. article, video vs. podcast). If a source doesn't
obviously fit either (unlikely, but possible), use judgment and default to whichever
reference file's structural assumptions are closer to true for this source, or ask.

## If a summary/emphasis was given

Treat it as an active steer, not background color: let it shape which parts of the source
get segmented into their own pages, which get more depth, and what to look for while
reading — the same way you'd weight a topic differently if someone told you in advance
"pay attention to X" versus reading cold. It does not change any of the mechanics below.

## Run §4 exactly as written

1. **Read the full source**, chunking by natural structure (see the matched reference file
   for what "natural structure" means for this source type) rather than arbitrary token
   windows, if it's long enough that chunking is needed at all.
2. **Segment into distinct wiki pages**, defaulting to editing an existing page over
   creating a new one (§3.1) — most sources earn several pages, not one.
3. **Write each page** with complete frontmatter (§2) and an honest `extracted` confidence
   tag.

   **Default landing folder is `wiki/claude-knowledge/`, not `wiki/shared/`** (§3.2) — this
   is true regardless of who supplied the source file. The one exception: if the source
   itself is Alfonso's own authored material (his own notes, his own raw file expressing
   his own views), it's `shared` immediately. Everything else — a book, article, or
   transcript some other author wrote or said — lands in `claude-knowledge` and stays there
   until a later `interrogate-me` pass verifies Alfonso's own grasp of it.
4. **Preserve real depth** per §4 point 2 — the actual mechanisms, caveats, and examples,
   not a compressed summary of conclusions.
5. **Apply `shared`/`claude-knowledge` pairing only where earned** (§3.2) — never mint
   stubs on the other side just for symmetry.
6. **Update `index.md` and `log.md`.**
7. **Close with the mandatory self-verification pass** (§4 point 4) — check both
   faithfulness (is each claim true to the source) and whether anything got flattened (did
   the source's actual reasoning and nuance make it onto the page, or just its conclusions).

No per-page confirmation is needed anywhere in this — handing the source over and running
this skill is itself the instruction to write, per §4.

## After ingestion finishes

Mention to the user that an `interrogate-me` pass on this source is a natural next step, if
one hasn't already been discussed — that's what would let any of the freshly-ingested
`claude-knowledge` pages earn a `shared` counterpart. Don't run it automatically as part of
this skill unless told to; offering it is enough.
