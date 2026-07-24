# Offering an `interrogate-me` Pass After Ingestion

Read this at the close of an `ingest-source` run, right after self-verification (main
`SKILL.md` step 7) is done.

## When and how to offer

Once, immediately, as a single line — keep the offer itself cheap, not ceremony:

> Want me to run an `interrogate-me` pass on this now, to see what you already know and
> lock that in?

Wait for a yes or no. This is not optional politeness — `interrogate-me`'s own `SKILL.md`
(step 0) requires consent before Claude starts an interrogation it noticed the opportunity
for itself, as opposed to one Alfonso asked for directly. Ingestion finishing counts as
"Claude noticed the opportunity," so the same rule applies here.

If yes, decide where it happens next (below). If no, stop — don't re-offer later in the same
session.

## Where it happens: same session by default, fresh chat as the fallback

**Default: continue in the current session immediately**, right after the offer is
accepted. No handoff needed for the common case.

**Fallback: a fresh chat**, if this session's context is already substantial — Alfonso's
own practical marker is roughly **50% of the context window used**, checked by him via
Claude Code's own context indicator. This isn't something Claude can check on its own (no
tool exposes it); Alfonso makes this call and says so if a handoff is the better option.

**Always a fresh chat, never `/compact`.** Compaction summarizes the *entire* prior
conversation indiscriminately — it can't selectively discard the parts irrelevant to this
specific source. A session that's covered several unrelated topics (wiki maintenance,
other ingestions, design discussions) would carry all of that forward as compressed noise
sitting alongside the signal the interrogation actually needs — this is close to the
"distractor" effect documented in `wiki/claude-knowledge/context-rot-research.md`, and
unlike a clean fresh start, it can't be stripped back out afterward. A fresh chat with the
handoff prompt below is not the expensive option it might seem — the handoff is built to
be cheap (pointers, not pasted content), so there's no real reload cost being traded away
by choosing it over compaction.

## The handoff prompt, if going to a fresh chat

Include exactly these four things, and keep it to pointers — the fresh session reads the
actual wiki pages itself, on its own schedule (see below), rather than having them pasted
in:

1. **What was just ingested** — the source's identity and its `raw/` file path.
2. **The specific wiki pages this ingestion produced** — one line each: title, path, and a
   one-sentence description of what it covers. This is enough for the fresh session to know
   the source's actual sub-structure without reading full content yet — `interrogate-me`
   step 2 (cued follow-up) needs to know that structure to walk it properly.
3. **Any emphasis or summary Alfonso gave the original ingestion request**, carried forward
   unchanged, so the interrogation doesn't lose framing the ingestion itself was given.
4. **A pointer to `CLAUDE-WIKI.md` §10.3–§10.4** for the importance-scoring mechanic that
   governs how much of this interrogation's output should fold into `ABOUT-ME.md`.

**Explicit instruction to include in the handoff:** read a given wiki page's full content
only when the interrogation actually reaches that specific sub-topic — not all of them
loaded in bulk before the first question. This keeps working context small at any one
point and matches `interrogate-me`'s own broad-then-narrow, one-sub-topic-at-a-time
sequencing (`SKILL.md` §3) rather than front-loading everything the pages contain before
knowing which parts will actually come up.

## Example handoff prompt

> Run an `interrogate-me` pass on Alex Hormozi's *$100M Offers*, just ingested from
> `raw/2026-07-22-100m-offers-hormozi-audiobook-transcript.md`. It produced these wiki
> pages — read each one in full only when the interrogation actually reaches that
> sub-topic, not all at once:
>
> - `wiki/claude-knowledge/grand-slam-offer-framework.md` — core definition, commoditization
>   vs. differentiation, the 22.4x money-math example.
> - `wiki/claude-knowledge/finding-a-starving-market.md` — the four market indicators,
>   niching down.
> - *(...remaining pages, same format...)*
>
> No summary/emphasis was given for the original ingestion. Follow `interrogate-me`'s
> `SKILL.md` directly — assess first, cued follow-up through each page's actual structure,
> checkpoint before writing anything. At the close, per `CLAUDE-WIKI.md` §10.3–§10.4, ask
> Alfonso to rate this topic's importance 1–10 and use that to scale how much (if anything)
> folds into `ABOUT-ME.md`.
