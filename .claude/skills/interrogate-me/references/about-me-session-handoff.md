---
title: ABOUT-ME.md Cold-Start Session — Handoff Instructions
prepared: 2026-07-21
prepared_by: A prior Claude Code session, rewriting Alfonso's own handoff draft to fix a
  workflow mismatch (batched rounds vs. one-question-at-a-time) and to point directly at
  the research brief that already exists for this session
---

## Instructions to paste into the new chat

Use the `interrogate-me` skill for this session. Read `.claude/skills/interrogate-me/SKILL.md`
in full, then `references/about-me.md` — this session is the `ABOUT-ME.md` cold start (the
file is currently empty), and that reference file governs this exact case. `references/about-me.md`
itself points to `references/about-me-topics.md`, a content-scope brief prepared by a prior
session that already covers what to ask about and why — you don't need to wait for that
research to be "supplied" separately, it's already sitting in the reference chain.

## Scope

This is the broad-first sweep, not a narrow one — start general across Alfonso's life and
work, then narrow into whatever's worth a deep pass. Use `references/about-me-topics.md`
alongside your own read of what comes up during the sweep to decide which topics earn that
depth — that file tells you what to cover, not how to run the session; the rest of this
document is the how.

**One topic is mandatory regardless of what else comes out of the sweep or the research:
Alfonso's current business understanding and knowledge.** Give it a real deep pass no
matter what.

## The interaction pattern for this session — read this carefully, it changes SKILL.md's default

`SKILL.md` step 3 defaults to one specific question at a time, and says why: bundling
several questions into one message lets someone dodge the hard part and answer the easy
part instead. That reasoning is sound in general, and for a live back-and-forth
conversation it's the right default. **It is deliberately overridden for this session.**

Alfonso works this project through multi-chat handoffs — step away, answer in depth, come
back — and wants that same pattern here: **rounds of grouped, open-ended questions, not a
single-question ping-pong.** Concretely:

- Each round is a **batch of roughly 5–10 open-ended questions**, grouped by topic thread
  (e.g. 2–3 questions on one life area, 2–3 on another), not an undifferentiated list. Lean
  toward the upper end of that range when a topic naturally supports it — don't pad with
  filler just to hit a number, and don't split one coherent thread across two rounds just
  to stay under 10.
- Every question in a round should be **open-ended** — built to be elaborated on at
  length, not answered in a phrase. Ask for the reasoning, the example, the "walk me
  through it," not just the fact.
- Present the whole round as one message. Wait for Alfonso to answer all of it in one
  pass before responding — don't reply after each individual answer within a round.
- **This is where the dodging risk that step 3 warns about gets handled instead of
  avoided**: after a full round comes back, look at what was thin, vague, or skipped, and
  make that the explicit target of specific follow-up questions in the *next* round. The
  drill lands a round later than it would in live back-and-forth, not never — the
  batching trades immediacy for Alfonso's preferred rhythm, it doesn't drop the mechanism.
- Multiple rounds are expected and fine — some questions genuinely depend on what an
  earlier round surfaces. Keep going in rounds until you've hit the sufficiency signal
  below, not until one round happens to feel complete.

Everything else in `SKILL.md`'s core technique still applies, just distributed across
rounds instead of single exchanges:

- **Assess before you reveal anything** (step 1) — every question, in every round, asks
  for Alfonso's own unprompted view first. Never lead with your own hypothesis, a source
  document, or your own read on a topic before he's answered independently.
- **Free recall is a floor, not a ceiling** (step 2) — don't treat what a round surfaces
  as the edge of what's there. If a topic has real structure (a book's actual arguments, a
  venture's actual timeline), walk it deliberately in a follow-up round rather than
  stopping because the open questions dried up.
- **Anchor in concrete specifics** (step 3's other guidance, unaffected by the batching
  change) — "tell me about the actual time this came up," not hypotheticals.

## Knowing when you have enough, and finishing

You have enough on a given area when new answers stop adding information and anything
genuinely ambiguous has been explicitly resolved (SKILL.md step 6) — not before.

**Never end unilaterally.** Once you've hit that signal, show Alfonso a synthesized draft
of what's been extracted — not a transcript of the rounds — and ask whether it's complete
or needs correction. Loop on this, including further rounds of questions if the checkpoint
surfaces gaps, until he actually confirms it's done. You don't get to decide alone that the
session is finished.

## Writing it down

Only after Alfonso confirms the draft at that checkpoint: write directly to `ABOUT-ME.md`,
no separate approval gate needed on top of that confirmation — this is ungated per
`references/about-me.md`, but only *after* the checkpoint clears, not before.

- **Preserve real depth.** His actual phrasing, his actual examples, the reasoning behind
  a claim — not a compressed summary of conclusions. A technically accurate one-line
  version of something he explained at length has still lost what made it useful.
- **No raw transcript, ever, anywhere.** The only artifact that persists is the polished,
  synthesized write-up from the confirmed checkpoint draft.
