---
name: interrogate-me
description: Interrogates the user in sustained depth to find out what they actually know, believe, or understand about a topic, then extracts it into a detailed written account for later use. Use when the user asks to be interrogated, grilled, drilled, quizzed, or questioned in depth about a topic — e.g. "interrogate me about X", "grill me on X", "drill me on X until I get it", "quiz me on that book", "test my knowledge of X". Also use proactively when noticing an ambiguous point worth asking the user about directly, or a gap in their understanding that matters for the work at hand. Not for one-off factual questions, product/design requirements-gathering, or interrogating a system, API, or codebase rather than the user's own knowledge.
---

# Interrogate Me

## What this skill does

Finds out what someone actually knows, believes, or understands about a topic — not by
asking once and taking the first answer at face value, but by assessing their real depth
first and then extracting it into a comprehensive account that's actually useful later.
Two things happen, in this order, in every session:

1. **Assess** — find out what's really there, including the parts the person wouldn't
   think to mention unprompted.
2. **Extract** — turn that into a detailed, faithful written account, not a compressed
   summary of conclusions.

This is a general-purpose technique, not a single-use script. It gets applied differently
depending on what's being assessed (a person's grasp of a book vs. their own life story vs.
one specific ambiguous claim), but the underlying technique — how questions are sequenced,
how depth gets tested, when to stop, what the output looks like — stays the same. If the
project or context you're working in has already written down specific applications of
this technique (check for a `references/` folder alongside this file), read the matching
one and layer its specifics on top of everything below — it will tell you exactly where
the output goes and what additional format or approval rules apply there. Don't invent that
part; the technique below is deliberately silent on destination because it changes per
context.

## The core technique

### 1. Assess first, reveal nothing

Before you show your own read on the topic, your hypothesis, a source document, or
anything else that could anchor the person's answer, ask them to state their existing
understanding unprompted. Showing your hand first defeats the point — people echo back
whatever they were just shown rather than surfacing what they actually independently
think. Get the unprompted version before revealing anything.

### 2. Free recall is a floor, not a ceiling

What someone volunteers unprompted, especially on a substantial topic (a whole book, a
broad area of their life, a complex domain), will almost always undershoot what they
actually retain — nobody recalls everything they know just because they were asked an open
question. Treat the free-recall answer as an honest starting point, not as the edge of
their knowledge. After it dries up, move to **structured, cued follow-up**: walk
deliberately through the topic's actual sub-structure (a book's chapters or core arguments,
a domain's named sub-concepts, a life area's typical components) and ask about each piece
specifically, rather than only following wherever the free-recall answer happened to lead.
Your final assessment of their depth should reflect this cued pass, not just what came out
unprompted.

### 3. How to actually ask

- **Sequence broad, then narrow.** Open with general framing and descend into specifics —
  don't lead with a narrow question before establishing the shape of the whole topic.
- **One specific question at a time.** Resist bundling several questions into one message;
  it lets people dodge the hard part and answer the easy part instead.
- **Anchor everything in concrete specifics, never hypotheticals.** "Tell me about the
  actual time this came up" beats "what would you think if." Hypothetical questions get
  hypothetical (i.e. weightless) answers.
- **Chase vague answers down to specifics.** "Some things," "sometimes," "kind of" are not
  answers — they're a prompt for your next question. Keep pushing until a generality
  resolves into something concrete: who, when, how many, which one.

### 4. Drilling on a shallow answer

When an answer feels thin, don't just re-ask the same question — escalate through these
layers, in order, stopping once you've actually gotten somewhere:

1. **Clarify** — pin down terms, ground the claim in a concrete example.
2. **Assumptions** — what's being taken for granted here?
3. **Evidence** — what actually supports this? Could it be shown wrong?
4. **Implications** — if this is true, what follows from it?
5. **Counterarguments** — how would this look argued from the other side?

Do this collaboratively, not adversarially. The goal is to help the person think more
clearly and to find out what's really there — not to catch them out or win an argument.
"I don't know" is a genuine, useful answer at any layer; record it as a real gap rather
than pushing until they invent something just to satisfy the question.

### 5. No adversarial pushback as a separate mechanic

Don't bolt on a distinct "devil's advocate" or confrontational mode beyond what's already
in step 4 (pressing for more depth on a thin answer). Ordinary disagreement — if you think
something's actually wrong — still applies exactly as it would in any other conversation;
it isn't suppressed by being in an interrogation session, but it also isn't manufactured
just because the session calls for depth.

### 6. Knowing when you have enough

You have enough on a given sub-topic when new answers have stopped adding information
(you're hearing the same things restated) and anything genuinely ambiguous has been
explicitly resolved rather than quietly assumed. That's your internal signal to move to
the checkpoint below — it is not, by itself, a reason to stop the session or write
anything.

### 7. Always checkpoint before finishing — never end unilaterally

Once you've hit the sufficiency signal, show the person a synthesized draft of what you've
extracted — not a raw transcript of the back-and-forth — and ask whether it's complete or
whether they want to add or correct something. Keep looping on this until they confirm
it's done. You never get to decide alone that a session is finished; you only get to decide
when it's ready to show them.

### 8. What the output actually looks like

- **No raw transcripts.** The only artifact that persists is the polished, synthesized
  account from step 7 — never a log of the questions and answers themselves.
- **Preserve real depth — don't flatten to conclusions.** If the session surfaced
  reasoning, caveats, concrete examples, or nuance, the written account needs to carry
  that, not compress it into a tidy one-line summary. A summary that's technically accurate
  but has lost the texture of what was actually said has failed at this skill's actual job,
  which is to leave behind something genuinely useful for later — not a clean abstract.
- **Update existing accounts rather than duplicating them.** If this topic already has a
  written account from an earlier session, revise it in place to reflect what's new or
  changed. Don't leave a stale version sitting next to a fresher one.

## Example

Alfonso says "grill me on the negotiation book I read."

- **Assess first:** "Before I ask anything specific — in your own words, what's the core
  approach that book argues for, and what's one idea from it you've actually used since?"
  Not "did the book say X" — that would anchor him to a specific claim before he's answered
  independently.
- **Free recall is a floor:** he names one technique and a rough shape of the argument.
  That's a starting point, not the ceiling — follow up by working through the book's actual
  structure ("it also covers preparation, anchoring, and walking away — what's your read on
  each of those?") rather than stopping because the open question dried up.
- **Drilling a thin answer:** he says "anchoring is about starting high, I think." Clarify
  what "high" means in his own words, ask what happens if the other side anchors first
  (implication), ask what the book says can go wrong with it (evidence/counterargument).
- **Checkpoint:** once new answers stop adding anything, show him a synthesized draft — his
  actual understanding of the book, organized by the book's own structure, in his own words
  and examples — and ask if it's complete.

## If something's not working

- **Answers stay one-word or disengaged.** Don't keep re-asking the same way — narrow to
  something concrete and low-effort ("what's the one part of this you actually remember
  clearly?") rather than repeating an open question that isn't landing.
- **The person contradicts something they said earlier in the same session.** Surface it
  directly rather than quietly picking one version: "you said X a minute ago, and now Y —
  which is closer to what you actually think?" That's ordinary clarification, not
  confrontation.
- **The topic turns out to be too small for this technique.** If it's clear after a few
  questions that there's just one straightforward fact to confirm, say so and wrap up
  rather than manufacturing five layers of drilling out of a topic that doesn't have that
  much depth. This skill is for sustained depth, not for padding a simple exchange.
- **A session is dragging with no end in sight.** If you've drilled through several layers
  and answers are just restating what's already been said, that itself is the sufficiency
  signal (step 6) — treat it as "enough," not as a reason to push harder.

## Applying this in a specific context

The steps above are the whole technique, deliberately without an opinion on where the
output ends up or what approval process, if any, governs writing it there — that's
context-specific. Before finishing a session, check whether `references/` (next to this
file) contains a file matching what you're being asked to do here. If one exists, follow it
for the destination, format, and any write-approval rules on top of everything above. If
none exists, use your judgment: ask the person where they want this written down, or just
give them the finished account directly in conversation.
