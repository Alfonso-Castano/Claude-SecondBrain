# Applying interrogate-me: testing retained knowledge of a wiki topic

Use this when the interrogation is meant to find out how well Alfonso actually understands
a topic that's already been ingested into the wiki — a book, a domain, a concept — as
distinct from what the wiki itself contains. This produces an honest model of Alfonso's own
grasp, separate from the wiki's content, and it's the one application of this skill that's
assessment in the fuller sense, not just extraction.

## Why this exists

Two concrete uses, both matter:

1. **Points Alfonso at his own gaps.** If he doesn't have a solid grasp of something the
   wiki says is important, that's worth him knowing so he can go learn it — the point is
   for him to be able to guide and check the work, not just delegate it.
2. **Calibrates how much Claude should carry vs. explain.** When Claude is doing real work
   on a topic (e.g. marketing for a venture) and knows Alfonso's grasp of the relevant
   concepts is thin, it should account for that — offering more explanation, checking in
   more, not assuming shared footing it doesn't actually have. This is topic-specific
   context, distinct from ABOUT-ME.md's general, always-true personal context.

## Technique specifics for this application

Layer these on top of SKILL.md's core technique:

- **Baseline before revealing (SKILL.md step 1, applied specifically here):** have Alfonso
  state confident, specific claims about the topic before Claude reveals anything it
  independently knows. This is the actual baseline the rest of the session measures against.
- **Test understanding, not recall.** Favor why / how / contrastive-why ("why does X happen
  but not Y") / mechanism ("how does X lead to Y") / connection / prediction prompts over
  bare factual-recall questions. A question with a single correct factual answer tests
  memorization, not understanding — it's not useful here.
- **Judge grasp by what can be defended, not by confidence.** "I know a bit about this" is
  not the same as being able to back a claim with specifics under a follow-up question.
  Confidence is not signal; specificity under pressure is.
- **Close each sub-concept plainly, in this order:** state the grasp verdict, credit what's
  genuinely solid (specifically — cite what they actually said, not generic praise), name
  the gap concretely, then move to the next sub-concept. Frame the whole thing as "here's
  what's worth reviewing," never as a grade or score — that's not what this is for.

## Where the output lives

A single companion file per topic, living in `wiki/shared/`, next to that topic's existing
`shared/` (and `claude-knowledge/`, if paired) page(s). Not a new top-level folder — this
was deliberately rejected as unneeded complexity.

**Structure — per sub-concept, not one blanket rating for the whole topic:**

```markdown
## [Sub-concept name]
- **Grasp:** [e.g. solid / partial / shaky / untested]
- **What's solid:** [specific things Alfonso demonstrably understands, with what he actually said]
- **What's shaky or missing:** [specific gaps, concrete enough to act on]
- **Last tested:** [date]
```

A single overall rating for the whole topic isn't enough — "what should I review" needs
something concrete to point at, which only a per-sub-concept breakdown gives.

**No confidence-tag/citation machinery from CLAUDE-WIKI.md §2.** `extracted` / `inferred` /
`ambiguous` describe faithfulness to a source claim; this file describes Alfonso's grasp of
a claim, which is a different kind of statement entirely and doesn't need a citation
bottoming out externally.

**Discoverability:** link to this file from the topic's `shared/` page(s) so it surfaces
under CLAUDE-WIKI.md §5's index-first discipline, and add a one-line mention in `index.md`
— Alfonso wants to actively browse this to find review targets, not just have it sit as
passive background context for Claude.

## Whether it's gated

Write directly, ungated — same reasoning as ABOUT-ME.md: this is diagnostic content about
Alfonso's own understanding, not a claim about the world, so it was never really a "wiki
write" under CLAUDE-WIKI.md §7's original definition. SKILL.md step 7's completeness
checkpoint still applies before writing; it's the write itself, after that checkpoint,
that's silent.

## Revising over time

Per SKILL.md step 8: when Alfonso is retested on a topic later (he's learned more, or it's
just been a while), update the relevant sub-concept entries in place — including the
`Last tested` date — rather than appending a new, separate record.
