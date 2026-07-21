---
title: What Should Go Into ABOUT-ME.md — Topic Brief
prepared: 2026-07-21
prepared_by: A prior Claude Code session in this project, at Alfonso's request, before the cold-start ABOUT-ME.md interrogation session
---

This document exists because `references/about-me.md` (in this same folder) tells whoever
runs the cold-start interrogation to "research what tends to belong in a personal-context
file for a system like this one" before starting — but neither Alfonso nor a fresh session
necessarily knows what that research would turn up. This is that research, done once, so
the interrogating session doesn't have to re-derive it from nothing. Read this alongside
`references/about-me.md` (process) and `SKILL.md` (core technique) — this document is
**content scope only**: what to ask about, and why each area matters for this specific
project. It does not change how to ask (that's `SKILL.md`'s job) or where the output goes
or whether it's gated (that's `references/about-me.md`'s job).

## What ABOUT-ME.md is for, precisely

Per `CLAUDE.md` and `CLAUDE-WIKI.md`: `ABOUT-ME.md` is always-true, root-level personal
context about Alfonso — loaded into most sessions automatically, structurally separate from
the on-demand wiki (`wiki/shared/`, `wiki/claude-knowledge/`). It is **not** a topic-indexed
knowledge archive (that's the wiki's job) and **not** a record of project design decisions
(that's `.context/DECISIONS.md`'s job, and out of scope for this interrogation entirely —
`.context/` is feature-workflow tooling, not part of the second brain's own operation). It
is a model of **Alfonso himself** — who he is, how he works, what he knows, what he's
building toward — durable enough that any session, cold, can read it and immediately
understand who it's talking to and how to be useful to him specifically, without
re-deriving that from scratch or from this project's own design docs.

## What's already known — don't re-ask this from scratch

A separate source document (`raw/2026-07-21-second-brain-for-me.md`) already establishes a
real amount of this, and it's already been read by the session that built this project's
operating rules. The interrogation should **build on and verify/deepen** these, not
re-extract them as if starting cold — but should still surface them for Alfonso to
elaborate on, since a one-line prior summary is exactly the kind of "free recall floor, not
ceiling" `SKILL.md` step 2 warns against treating as complete:

- **Background:** a computer science student with real strength in conceptual thinking,
  problem framing, and applied AI/agentic work — hands-on with Claude Code and context
  engineering specifically. Close to a beginner in business specifically, with two
  loosely-retained sources so far (Hormozi's *$100M Offers*, a negotiation book).
- **Two prior ventures**, both instructive but in different ways: one stalled on
  *distribution*, not on building; one *failed from over-delegating creative and strategic
  decisions to AI* with minimal human oversight — this second failure is the direct cause
  of most of this project's design (propose-then-confirm, deferred automation, manual
  source validation).
- **Standing preference, stated directly and repeatedly:** honest evaluation over
  validation. Engages well with structured pushback, doesn't want to be told what he wants
  to hear, treats disagreement as useful.
- **Working style:** prefers depth over compression in answers and synthesis. Works
  deliberately and collaboratively — engages with structured option sets, revisits earlier
  decisions rather than treating them as final, would rather flag something as open than
  force a premature resolution. Uses multi-chat workflows deliberately (a context-rich
  backend chat, a focused-output chat, distilled context handed between them) — this
  project itself was built that way.
- **Interaction mode:** Claude Code sessions pointed at this folder, no separate frontend;
  Obsidian now adopted, but purely as a visual layer over the same files, not a different
  way of working.
- **Directional, not current:** has floated this second brain potentially becoming the
  backbone of a broader agentic operating system long-term — worth knowing as context, not
  something to interrogate deeply now.

Treat the above as a floor the interrogation confirms and deepens (ask him to elaborate,
give concrete examples, correct anything that's drifted) — not as settled enough to skip.

## The one mandatory topic, regardless of what else gets covered

`references/about-me.md` already names this explicitly, and it's worth restating here with
its reasoning: **Alfonso's current business understanding and knowledge** gets a full,
deep pass no matter what else this session covers. The entire second brain revolves around
functioning as a knowledgeable co-founder for ventures he hasn't built yet — Claude cannot
calibrate how much to explain, where to push back with independent knowledge versus where
it would be teaching him something he already has solid footing on, without an honest,
specific model of what he actually knows versus what he's absorbed loosely. This isn't
"does he know business" as a yes/no — it's per-concept: what from Hormozi's book has he
actually internalized versus skimmed, what negotiation principles can he apply versus just
recite, where are the two failed ventures' lessons actually integrated into how he'd
approach the next one versus just known as a story he can retell.

## Topic areas worth covering, and why each matters here specifically

These are drawn from two independent places: (1) the general "personal user manual" /
"manager README" pattern — a well-established practice for exactly this kind of
"how do I work, what should you know about me" document, just usually written for human
colleagues rather than an AI — adapted for what actually matters when the "colleague" is an
AI meant to function as co-founder; and (2) what this project's own design already implies
matters, read from `raw/2026-07-21-second-brain-for-me.md` and `CLAUDE-WIKI.md` directly.

### Business and venture context (beyond the mandatory topic above)

- Specific details of the two prior ventures — not just "one failed from over-delegation,"
  but what the actual business was, what stage it reached, what the over-delegation
  concretely looked like in practice (which decisions, what the AI did, what Alfonso
  wishes he'd caught earlier), and the same depth for the distribution-stalled one.
- Industries, business models, or problem spaces he's actually drawn to or has been
  thinking about — this second brain is explicitly meant to be cross-venture, so knowing
  the shape of what he tends to gravitate toward (not just what he's already built) matters.
- Risk tolerance and decision-making style when facing genuine business uncertainty —
  distinct from his stated preference for AI pushback; this is about *his own* instincts
  under real ambiguity, which the AI needs to know in order to calibrate how hard to push
  back and on what.

### Working style and collaboration (deepen what's already known, don't just restate it)

- Concrete examples of "honest evaluation over validation" actually working well for him
  versus a time it didn't land — the abstract preference is already recorded; what it looks
  like in practice, in his own words, is what makes it usable.
- How he prefers disagreement to be delivered — direct and blunt, or reasoned-and-optioned
  (this project's devil's-advocate design already assumes reasoned-and-optioned; worth
  confirming that's actually his preference and not just this project's own default).
- What actually demotivates or frustrates him in a working relationship (per the
  "manager README" pattern's "what demotivates me" / "pet peeves" categories) — adapted:
  what would make him trust or disengage from an AI collaborator specifically.
- Focus patterns, if relevant to how sessions should be paced or structured — not
  mandatory, include only if it comes up naturally.

### Values and blind spots

- What he values in a thinking partner or collaborator, human or AI — directly informs how
  Claude should behave across this whole project, not just within the second brain.
- Self-identified blind spots or areas he knows he needs outside perspective on — the
  "manager README" pattern treats this as a distinct, valuable category from general
  self-description, and it's a natural target for the interrogation's "drilling on a thin
  answer" technique (SKILL.md step 4) since blind spots are, by nature, easy to
  under-report if only asked about directly once.

### Life and work context, at whatever depth feels natural

- Current work/school situation, in enough concrete detail that a session cold-starting
  months from now understands his actual day-to-day constraints, not just his abstract
  identity as "a CS student."
- Anything about how ventures fit into his broader life and goals — this second brain is
  explicitly meant to track an evolving model of Alfonso, not a siloed archive per venture,
  so the connective tissue between "who he is" and "what he's building" belongs here, not
  buried inside individual venture folders.

## What NOT to cover here

- Anything that's really about *this project's own design or rules* — that's
  `.context/DECISIONS.md` and `CLAUDE-WIKI.md`'s territory, not `ABOUT-ME.md`'s.
- Domain/business knowledge suitable for the wiki (e.g. a deep dive on a specific
  framework, book, or concept) — that belongs in `wiki/shared/` or `wiki/claude-knowledge/`
  via the normal ingestion path, not folded into `ABOUT-ME.md` just because it came up
  during this session. If something like that surfaces mid-interrogation, note it as a
  candidate for separate ingestion rather than writing it into `ABOUT-ME.md` directly.

## A closing note on scope

This is a cold-start brief for a first, broad pass — per `references/about-me.md`, `ABOUT-ME.md`
is meant to keep growing afterward through smaller follow-up sessions and ordinary
conversation. Not everything above needs to be exhausted in one sitting. If a topic runs
deep and interesting, let it — depth is the whole point (`SKILL.md` step 8) — and leave
what doesn't get reached for a later, narrower session rather than rushing to cover every
bullet above shallowly.
