# Second Brain — For Me: Purpose, Person, and Use

## Purpose of this document

You're reviewing a freshly-built second brain file base. Alfonso is also giving you a separate, extensive summary of what the second brain should technically consist of. This document is different: it's about **who this is for and why**, so that when you're reviewing the file base, you're not just checking "does this match the spec," but "does this actually serve what this specific person needs." Use it to evaluate the build, not just to inform it — flag anywhere the built structure technically matches the summary but would still fail Alfonso in practice, given what's below.

---

## Who this is for

Alfonso is a computer science student with real strengths in conceptual thinking, problem framing, and applied AI work — hands-on experience with agentic workflows, Claude Code, and context engineering specifically. He's not a business novice by disposition, but he is by knowledge: close to a beginner in business specifically, with only two loosely-retained sources (Hormozi's *$100M Offers*, a negotiation book) informing what he currently knows.

## Why this exists

Two prior venture attempts sit behind this project, and they point in different directions:

- One stalled on **distribution**, not on building — the technical work wasn't the bottleneck.
- One **failed from over-delegating creative and strategic decisions to AI**, with minimal human oversight.

The second failure is the one that actually shaped this project's design. It's not a footnote — it's the reason nearly every mechanism in this system (propose-then-confirm, manual source validation, deferred automation) exists in the form it does. If the built file base has any path where Claude makes a strategic or creative call without Alfonso in the loop — beyond the one narrow, explicitly-named exception for initial source ingestion — that's a regression to the exact failure mode this project was built to avoid, not a minor implementation detail.

## What Alfonso wants this to function as

Not a note-taking app, and not a passive archive. The stated goal, repeatedly: something that functions like an **executive assistant or co-founder** — capable of giving him new perspectives and genuinely pushing back on his ideas using its own independently-built knowledge, not just reflecting what he's already told it.

This shows up as a standing, explicit preference in how he wants Claude to behave generally, not just within this project: **he wants honest evaluation over validation, and he's said so directly, more than once.** He engages well with structured pushback, doesn't want to be told what he wants to hear, and treats disagreement as useful rather than unwelcome. A reviewing agent should evaluate the build with this in mind — if something in the file base looks like it would make Claude more agreeable or less willing to surface an inconvenient finding, that's worth flagging even if it wasn't explicitly specified against.

## How he intends to use it

- **Interaction happens through Claude Code sessions** pointed directly at the folder — no separate frontend, Obsidian purely optional and only if a felt need for visualization shows up.
- **He prefers depth over compression** — when getting an answer or a synthesis, he wants the real depth preserved, not summarized down for brevity's sake. This should show up in how wiki pages are written, not just in conversation.
- **He works deliberately and collaboratively** — he engages with structured option sets, revisits earlier decisions rather than treating them as permanently settled, and would rather flag something as open than force a premature resolution. The system should be built to accommodate revision, not assume every early choice is final.
- **He uses multi-chat workflows** — one chat as a context-rich backend, another for focused output, with distilled context deliberately handed between them. This entire second brain project was itself built this way (this working chat, a separate video-context chat, a business-foundation chat, and now the actual build-phase agent) — it's not incidental, it's how he actually works, and the second brain should be legible to that pattern: context should be extractable and handoff-able, not trapped in a way that only makes sense inside one continuous conversation.
- **Growth is meant to be continuous and cross-cutting**, not siloed. Lessons from one venture are meant to inform another — the second brain tracks an evolving model of Alfonso himself, not just a topic-indexed archive. He's explicit that more information feeding in is good by default, specifically because the indexing/retrieval layer is what makes that safe. Long-term, he's floated this potentially becoming the backbone of a broader agentic operating system — worth knowing as directional context, not something to build toward now.

## Standing principles that should be visible throughout the build

- **Human judgment stays central** to strategic and creative decisions — this is the project's core constraint, not a nice-to-have.
- **Automation is deferred** until a concrete need actually shows up; a prompt is not treated as a sufficient permission layer for autonomous action.
- **Adapt existing, proven tools rather than building from scratch** — this shaped how skills and workflow tooling were chosen throughout the project, and should be visible in how the wiki's own skills (like grill-me) get built.
- **Don't over-optimize before starting** — Alfonso has said directly that he'd rather begin using the system and fix what needs fixing based on real experience than keep refining the design preemptively. A review that finds the build erring toward simplicity where something was genuinely undecided is not a problem; a review that finds it erring toward heavy, speculative infrastructure without a felt need behind it is worth flagging.

## What to actually check

When reviewing the file base against this document, the most useful thing you can do is look for places where the build is *technically compliant but practically wrong for this person* — for example: wiki pages that read as compressed summaries rather than preserving depth; anything that would make Claude more agreeable rather than more willing to push back; any autonomous write path beyond the one named exception; structure that assumes a single continuous session rather than being legible across separate handoffs; or premature infrastructure built ahead of an actual need. Surface anything that fits that pattern, even if it isn't a literal spec violation.
