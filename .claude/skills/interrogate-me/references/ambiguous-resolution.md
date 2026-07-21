# Applying interrogate-me: resolving an `ambiguous` wiki tag

Use this when the interrogation is about resolving a specific `ambiguous`-tagged point in
the Second Brain wiki, whether during a deep-ingestion pass (CLAUDE-WIKI.md §4) or during
reconciliation (CLAUDE-WIKI.md §9).

## Scope

Keep this narrow and bounded: one specific ambiguous point per session, not a sweep of
every ambiguity in a pass at once. A single ingestion or reconciliation pass may run
several of these sessions back to back — that's fine — but treat each ambiguity as its own
interrogation with its own checkpoint (SKILL.md step 7).

## The one adaptation to the core technique

Apply SKILL.md step 1 ("assess first, reveal nothing") literally here: ask what Alfonso
recalls or believes about the specific point *before* showing him the ambiguous source
text or your own reading of it. Showing the ambiguous passage first anchors his answer to
whatever confused Claude in the first place, rather than surfacing what he actually
thinks independently.

## Sufficiency

Narrower bar than the other two applications of this skill: you have enough once the
specific ambiguity is resolved, unambiguously. This isn't a broad knowledge sweep — stop
as soon as the one point is genuinely settled, don't keep going looking for more to extract.

## Where the output goes, and whether it's gated

**If this session is embedded in a deep-ingestion pass (CLAUDE-WIKI.md §4):**
Write directly. This inherits the ingestion pass's own write license — §4 is the one place
in the whole wiki schema where writes don't wait for per-page confirmation, because handing
over a source to be ingested is itself the instruction to write. This interrogation session
doesn't create a new exception; it's just the mechanism for resolving one ambiguity inside
a pass that already has that license. The resolved understanding becomes the page content
(with proper frontmatter per CLAUDE-WIKI.md §2). Citation can read
`synthesized from conversation on [date]` (a valid citation form per this project's
OVERVIEW.md) if the resolution is genuinely new information from Alfonso, or point back to
the original ingested source if the ambiguity was really about how to read that source
rather than new information.

**If this session is embedded in reconciliation (CLAUDE-WIKI.md §9):**
Stays gated by propose-then-confirm, always — resolving the ambiguity does not itself
authorize the write. If the resolution would overturn existing wiki content, change a trust
tag, or resolve a genuine contradiction, it's high-stakes and routes through CLAUDE-WIKI.md
§8's independent-subagent devil's-advocate path before Alfonso decides. No matter how clean
or well-structured this session's output is, it does not substitute for that human decision
— §8 exists specifically because contested claims need a person weighing two independently-
argued stances, not a well-written proposal to rubber-stamp.

Either way, SKILL.md step 7's completeness checkpoint (show the draft, confirm it's enough)
happens first and is separate from whichever write behavior applies above.
