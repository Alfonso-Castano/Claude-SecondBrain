---
title: Zettelkasten and Atomic Notes — And a Correction to CLAUDE-WIKI.md
folder: claude-knowledge
tags: [second-brain, zettelkasten, atomic-notes, luhmann, correction]
created: 2026-07-21
last_updated: 2026-07-21
source:
  - https://zettelkasten.de/introduction/ (accessed 2026-07-21)
  - https://zettelkasten.de/posts/literature-notes-vs-permanent-notes/ (accessed 2026-07-21)
  - https://tinkeringprod.com/what-is-zettelkasten-a-complete-guide-to-connected-note-taking/ (accessed 2026-07-21)
confidence: inferred
---

## Why this page exists, and its confidence tag

`CLAUDE-WIKI.md` §3.2 already invokes Zettelkasten by name, twice: the new-page-vs-edit rule (§3.1) is described as following "Zettelkasten's atomic-note discipline," and the earned-not-mechanical pairing rule (§3.2) is justified by an explicit claim: *"This is the exact documented failure mode of the closest analogous pattern, Zettelkasten's literature-notes vs. permanent-notes distinction: mechanically minting an empty counterpart note degrades the whole index's signal."* Since this project's own operating schema already cites this source as grounding, checking that citation against the actual literature is exactly the kind of verification this ingestion pass exists to do — and it's the reason this page is tagged `inferred` rather than `extracted`: the correction below is Claude's own analysis of a gap between what `CLAUDE-WIKI.md` claims and what the sources actually say, not a fact stated in the sources themselves.

## The actual method

Developed by German sociologist Niklas Luhmann, who used a physical "slip box" of roughly 90,000 index cards to produce over 70 books and 400 scholarly articles. Popularized in modern PKM circles by Sönke Ahrens' 2017 book *How to Take Smart Notes*.

Core principles:

- **Atomic notes** — each note captures exactly one idea, concept, or insight. This constraint forces clarity and makes individual notes more versatile, since they can connect to multiple contexts without becoming unwieldy trying to cover more than one thing.
- **Unique identifiers** — Luhmann's own specific contribution was a discipline of unique addressing and dense cross-linking that turned a storage device into a *generative* one — the numbering/addressing system is what let new notes attach to old ones in ways that produced genuinely new connections, not just archival retrieval.
- **Deliberate linking** — every new note gets linked to existing notes it relates to. This is what separates the method from ordinary note-taking; a pile of atomic, unlinked notes is not a Zettelkasten.
- **Complete sentences, own words** — each note is written in full sentences, in the author's own words, so it can be understood and reused independently of the context it was written in.

## The literature-notes vs. permanent-notes distinction

Ahrens' book describes two categories of note kept in the slip-box:

- **Literature notes** — comments on selected/marked-down text, adding context and helping the person remember their thoughts when reading; the goal is summarizing the text plus the reader's own key takeaways.
- **Permanent notes** (sometimes "main notes") — process the literature notes further, analyzing how they connect to the person's own interests, thinking, and ongoing research.

## The correction: this is not "the exact documented failure mode" CLAUDE-WIKI.md describes

Having read the actual Zettelkasten-community discussion of this distinction directly, the terminology itself is genuinely **contested and inconsistently used even within that community** — Ahrens himself uses "permanent notes" in one place to mean literature notes *and* main notes together, and elsewhere to mean main notes *to the exclusion of* literature notes. Some practitioners (cited by name in the community's own writing — Christian and Sascha, prominent voices at zettelkasten.de) reject the distinction entirely and treat it as a single undifferentiated category: "there are only notes that are part of the Zettelkasten and all other notes."

The actual documented tension in that literature is narrower and different in kind from what `CLAUDE-WIKI.md` §3.2 claims. It's specifically: *if, when trying to write a permanent note, you find you have no new ideas beyond what the literature note already contains, should you skip creating the permanent note, or should you just reclassify the literature note as permanent?* That's a live, debated, unresolved question about **when a note graduates from one category to another** — it is not a documented failure mode about **mechanically minting empty counterpart notes for symmetry**, which is the specific claim `CLAUDE-WIKI.md` §3.2 makes and attributes to this pattern.

**What this means practically:** `CLAUDE-WIKI.md` §3.2's underlying rule — don't mint a stub `claude-knowledge` page just to mirror a `shared` page, because low-information stub files dilute an index's signal — is a perfectly sound rule on its own terms. It just isn't "the exact documented failure mode" of Zettelkasten's literature/permanent distinction; that's an overstated citation, not a wrong rule. The rule should be understood as this project's own independently-reasoned design choice, loosely inspired by a real but looser analogy to Zettelkasten's general discipline around not creating notes that don't earn their place — not as directly borrowed, settled doctrine from that community. This is worth a small, honest correction to `CLAUDE-WIKI.md`'s phrasing rather than leaving the overstated citation as-is; flagged for Alfonso's review rather than silently fixed, since edits to `CLAUDE-WIKI.md` itself are a wiki-adjacent schema change outside this ingestion pass's own scope.

## Why atomicity still matters here, on its own merits

Independent of the citation-accuracy question above, atomic notes and deliberate linking are real, well-established practice worth keeping as the actual grounding for `CLAUDE-WIKI.md` §3.1's new-page-vs-edit default: a new page earns its existence when it's a genuinely distinct entity or concept worth linking to from elsewhere, and a new fact about something that already has a page belongs on that page rather than starting a near-duplicate. That default is well-supported by the literature on its own terms — it just doesn't need the overstated "exact documented failure mode" framing to be justified.
