# CLAUDE-WIKI.md — Wiki Operating Schema

This is the authoritative schema for how every session reads from, writes to, and
maintains the Second Brain wiki. `CLAUDE.md` is a thin router that points here; the
operating rules themselves live in this file.

The wiki has two content folders — `wiki/shared/` and `wiki/claude-knowledge/` — plus a
single `index.md` at the **project root** (not nested under `wiki/`). Raw, unprocessed
source material lives in `raw/` and is never treated as wiki content.

One principle overrides everything below: **human judgment stays central to every
strategic and creative decision.** Where any rule in this file appears to work against
that principle, treat it as a defect to be flagged, not a license to sideline the human.

---

## 1. Core operating principles

These are standing rules. They are not conditional on launch, project phase, or workload.

- **The feature workflow (`/feature-discuss`, `/feature-plan`, `/feature-execute`,
  `/feature-quick`, etc.) governs building this project's own infrastructure and
  components — the kind of work Feature #1 was (scaffolding the wiki structure and this
  schema itself). It does not govern the second brain's ongoing knowledge operations.**
  Ingestion, query, lint, and reconciliation — everything this file (§4–§9) describes —
  run directly, in conversation, following this schema, with no feature ceremony wrapped
  around them. Reading a new source into the wiki is not "adding a feature"; it is the
  system doing its actual job. If a session finds itself reaching for `/feature-quick` to
  wrap an ingestion or lint pass, that is a misapplication of the workflow, not a
  reasonable default — stop and run the operation directly per this schema instead.

- **No automation on a timer — ever.** Nothing in this system runs on a schedule.
  Ingestion, linting, and reconciliation are all manually triggered, permanently. This is
  not a not-yet-automated state that will change once things are stable; it is the design.
  There is no cron, no watcher, no "run this nightly" step anywhere in any workflow. Every
  pass begins because a human asked for it.

- **Automemory is disabled for this repository** via `autoMemoryEnabled: false` in the
  repo-local `.claude/settings.json` (committed, repo-scoped). This does not affect
  automemory in any other Claude Code project on this machine. The wiki is the deliberate,
  reviewable memory of this project; automatic background memory would bypass the
  trust-tagging and propose-then-confirm discipline that the rest of this schema exists to
  enforce.

- **Every claim is traceable.** No page exists without a trust tag and a citation, and no
  citation is allowed to bottom out inside the wiki (see §2 and §6).

- **Writes are gated; disagreement is not.** Proposing a change to the wiki always waits
  for confirmation (with one named exception). Voicing disagreement in conversation never
  does (see §7).

---

## 2. Frontmatter template

Every wiki page — in `wiki/shared/` or `wiki/claude-knowledge/` — must open with YAML
frontmatter containing these fields:

```yaml
---
title: Human-readable page title
folder: shared            # shared | claude-knowledge
tags: [topic, another-topic]
created: 2026-07-15
last_updated: 2026-07-15
source: raw/2026-07-15-call-notes.md   # where this content bottoms out — see below
confidence: extracted     # extracted | inferred | ambiguous
paired_with: ../claude-knowledge/topic.md   # OMIT this field entirely if unpaired
---
```

Field notes:

- **`folder`** is `shared` or `claude-knowledge` and must match the folder the page
  actually lives in.
- **`confidence`** is the page's **trust tag** and is one of:
  - `extracted` — stated directly in the source; a faithful transcription of what the
    source said.
  - `inferred` — reasoned from the source but not stated verbatim; Claude connected dots.
  - `ambiguous` — the source is unclear, conflicting, or under-specified on this point.
- **`source`** is the **citation**. It must point to something **outside the wiki**: a
  file in `raw/`, an external research artifact, or a dated conversation. It may never
  point to another wiki page (see §6, citation-chain check).
- **`paired_with`** links a page to its counterpart on the other side of the
  `shared`/`claude-knowledge` divide. **If the page is unpaired, omit this field
  entirely** — do not leave it blank, `null`, or empty. Its absence is meaningful and is
  what the lint pass reads.

**Minimum bar:** no page may exist without, at minimum, a trust tag (`confidence`) and a
citation (`source`) that bottoms out outside the wiki. A page missing either is invalid
and must be fixed or removed, not shipped.

**One explicit exemption:** knowledge-testing companion files (one per topic, living in
`wiki/shared/` next to that topic's own page — see the `interrogate-me` skill's
`references/knowledge-testing.md`) are diagnostic content about Alfonso's own grasp of a
topic, not a claim about the world, and are exempt from the `confidence`/`source`
requirement above by design. A lint pass enforcing this minimum bar (§6.2) must recognize
this exemption rather than flagging these files as invalid.

---

## 3. Page structure rules

### 3.1 New page vs. edit — default to edit

Default toward merging into or editing an existing page rather than creating a new one.
This follows Zettelkasten's atomic-note discipline: each note is one idea, and related
facts accrete onto the note they belong to instead of scattering across near-duplicate
pages.

Create a **new** page only when the content is a genuinely distinct entity or concept —
something worth linking to from elsewhere in the wiki. A new person, a new company, a new
named concept, a new project: these earn a page. A new fact about something that already
has a page does **not**; it belongs on the existing page. Creating a page is not the
reflex for every new fact — editing is.

### 3.2 `shared` / `claude-knowledge` pairing — earned, not mechanical

The two folders can pair: a `shared` page (facts the human handed over) can have a
`claude-knowledge` counterpart (what Claude independently researched or concluded about
the same topic), linked via `paired_with`.

**A pairing is earned, never mechanical.** Never create a stub on the other side of a
pairing just to satisfy the convention. A `claude-knowledge` page exists only when Claude
actually has independent knowledge worth recording; a `shared` page exists only when the
human actually provided content. If one side has nothing substantive to say, it has no
page, and the existing side is simply unpaired (`paired_with` omitted).

The failure mode this avoids is **low-information stub files diluting the index** — pages
that exist only to complete a symmetry, carrying no real content, that a reader (human or
Claude) still has to open, evaluate, and dismiss. This is this project's own reasoning, not
a rule borrowed from established doctrine — it is only loosely analogous to Zettelkasten's
literature-notes vs. permanent-notes distinction (that community's actual documented
tension is narrower: *when* a literature note should graduate into a permanent note, not
whether to mechanically mint an empty counterpart for symmetry). See
`wiki/claude-knowledge/zettelkasten-atomic-notes.md` for the full correction and its
sourcing. The rule stands on its own merits regardless.

**A pairing must be visible as a real link, not just a frontmatter field.** Whenever a page
sets `paired_with`, it must also contain an actual inline relative markdown link (§3.3) to
its counterpart somewhere in the page body — not rely on the `paired_with` field alone.
This was added after Obsidian was adopted as a browsing layer for this wiki: Obsidian's
graph view and backlinks only render actual links, not arbitrary YAML frontmatter fields,
so a pairing that exists only in `paired_with` is invisible when actually browsing the
wiki, even though `CLAUDE-WIKI.md` treats it as a meaningful, earned relationship. The
frontmatter field remains required (it's what the lint pass's citation/pairing checks
read), but it is no longer sufficient on its own.

### 3.3 Links — relative markdown only, no wikilinks

Use standard relative markdown links between pages:

```markdown
See [Topic](../claude-knowledge/topic.md) for the researched view.
```

**Never use `[[wikilink]]` syntax.** There is no resolver for it in this project: a
visualization frontend (e.g. Obsidian) is deliberately deferred, so `[[…]]` links would
resolve to nothing and silently break navigation and link-checking. This has to be stated
explicitly because wikilink syntax is a plausible default carried in from general PKM
training data — it is the kind of thing a session might reach for by habit. Do not. Only
relative markdown links are valid here, and only they are checked by the lint pass.

---

## 4. Ingestion workflow (deep-ingestion pass)

Deep ingestion is the process of reading a source in `raw/` (or a handed-over document)
and writing its content into the wiki as properly-structured, trust-tagged pages.

**Deep ingestion is the one path that writes directly to the wiki without per-page
confirmation.** This is the single named exception to propose-then-confirm (§7). The
justification is that handing over a source to be ingested is *itself* an act of trust and
an explicit instruction to write: the human has already said "take this in." Pausing to
confirm each page would defeat the point of a bulk pass and manufacture confirmation
fatigue. So within a deep-ingestion pass, Claude creates and edits pages directly.

Because that human review is waived per-page, the pass carries its own discipline:

1. **Read and segment the source** into distinct entities/concepts, applying the
   new-page-vs-edit rule (§3.1) — merge into existing pages by default, create new pages
   only for genuinely distinct entities.
2. **Write each page** with complete, valid frontmatter (§2), including an honest trust
   tag and a `source` citation that points back to the ingested material.

   **Preserve depth — do not compress for brevity.** Alfonso has stated this directly and
   repeatedly: he wants a source's actual reasoning, nuance, caveats, and concrete examples
   preserved in the wiki, not distilled down to a tidy summary of conclusions. This is a
   personalization on top of the raw/wiki pattern, not something the pattern itself
   prescribes — the pattern is silent on how much detail to keep, and the default instinct
   under a workflow like this is to compress. Resist that instinct. If a source spends three
   paragraphs building an argument with examples, the wiki page should show that argument
   being built, not collapse it into a one-line conclusion. A page that is accurate but
   flattened has still lost something real: this rule exists because that loss is easy to
   commit without noticing, and correspondingly easy to leave unfixed unless it's checked
   for explicitly (see point 4).
3. **Apply pairing only where earned** (§3.2) — never mint stubs.
4. **Self-verification (the pass's own closing step).** After the batch is written, Claude
   re-checks its own ingestion batch for accuracy before considering the pass complete:
   did each page faithfully represent the source, are the trust tags honest, do citations
   resolve, did anything get garbled or over-claimed — **and, as a distinct check, did
   anything get flattened?** Faithfulness asks whether a claim is *true* to the source;
   the depth check asks whether the source's reasoning, nuance, and examples actually
   made it onto the page, or whether the page is a compressed summary that lost the
   texture of the original. A page can pass the faithfulness check and still fail the
   depth check — a technically-accurate one-sentence summary of a nuanced argument is
   exactly this failure mode. Both checks are required; neither substitutes for the other.

   Self-verification is **separate from trust-tagging** and is not optional polish. A
   trust tag describes Claude's confidence in a *claim* (was this extracted, inferred, or
   ambiguous?). Self-verification is Claude actually *checking its own work* — a different
   act entirely. Given that deep ingestion writes with **zero per-page human review**, this
   check is the structural counterweight to the waived confirmation. It is the pass's
   closing step, not something to skip when time is short. A deep-ingestion pass is not
   complete until self-verification has run.

The **"grill me" interrogation skill** (a future feature, not built here) plugs into this
workflow: it is the mechanism by which the human is actively questioned to surface source
material and resolve `ambiguous`-tagged points before or during ingestion. Reference it as
the interrogation dependency; do not design around its current absence.

---

## 5. Query workflow

When answering from the wiki:

- **Index-first discipline.** Read `index.md` (project root) **first**. Use it to locate
  the few pages actually relevant to the question, then drill into only those pages. Never
  load the whole wiki into context — the index exists precisely so you don't have to.
- **Trust-tag surfacing.** Whenever a claim from the wiki is cited back into conversation,
  surface its trust tag — not only when the source page itself is opened. If you tell the
  human something the wiki says, the human must be able to see whether that thing was
  `extracted`, `inferred`, or `ambiguous` at the moment you say it. An `inferred` or
  `ambiguous` claim stated with the same bare confidence as an `extracted` one is a
  trust-tag failure even if the underlying page is correctly tagged.

---

## 6. Lint workflow

Linting is manually triggered (§1) and runs deterministic tooling before any AI judgment.
Every lint pass includes all of the following.

### 6.1 Deterministic first step (non-AI)

Run the markdown tooling first, via the npm scripts already configured in `package.json`:

- `npm run lint:md` — `markdownlint-cli2` over the markdown.
- `npm run lint:links` — `markdown-link-check` over inter-page links.
- `npm run lint` — runs both.

These are deterministic and non-AI. They are the first step of every lint pass; the
AI-judgment checks below run only after the mechanical checks are clean (or their failures
are understood).

### 6.2 AI-judgment checks

- **Orphan-page detection.** Find pages that nothing links to and that link to nothing —
  pages stranded outside the wiki's link graph.
- **Index-entry-vs-page-content drift.** Detect where an `index.md` entry no longer
  matches the page it describes (stale summaries, renamed topics, moved content).
- **Citation-chain-bottoms-out-externally check.** Every `claude-knowledge` page's
  citation must trace **outside the wiki** — to a raw file, external research, or a dated
  conversation. A citation that resolves to another wiki page (directly or through a chain)
  is invalid: the chain must bottom out externally, never in the wiki itself.
- **`index.md` size/token trigger.** Flag the index for restructuring when it reaches
  **~150–200 entries or ~3–4k tokens**. Beyond that, index-first discipline (§5) starts to
  break down because the index itself no longer fits comfortably in working context.
- **Trust-tag enforcement.** Confirm every page carries a valid `confidence` tag and that
  tags are honest against their sources. This is the maintenance-side counterpart to the
  query-side requirement in §5 that trust tags be surfaced when claims are cited.

### 6.3 Proactive gap-surfacing

Lint is not only hygiene. A lint pass must also **proactively surface gaps and interesting
connections for new-article candidates** — pointing at what is worth researching or
ingesting next, not only fixing what already exists. Thin areas, topics referenced but
never written up, and non-obvious connections between existing pages are all lint output.
The lint pass should leave the human with suggestions of what to build next, not just a
clean bill of health.

---

## 7. Propose-then-confirm, and the write-only boundary

### 7.1 The rule

Propose-then-confirm governs **every wiki write**: creating a page, editing a page, filing
an ad-hoc conversational answer into the wiki, or applying a reconciliation update. For
any of these, Claude proposes the change and waits for the human to confirm before writing.

The **one exception** is the deep-ingestion pass (§4), where handing over a source is
itself the instruction to write.

### 7.2 The boundary — this gate applies to writes only

**This gate applies to writes only. It must never gate conversational pushback or
disagreement, which fires immediately and un-gated.**

This is called out as its own point because it is the easiest thing in this schema to get
wrong. Confirm-gating exists for exactly one purpose: to govern *what gets written into the
wiki*. It has nothing to say about how readily Claude voices a disagreement out loud. If
the confirm-gating instinct bleeds into conversation — if Claude starts softening, hedging,
or holding back disagreement because some part of it is "waiting for permission" — that
works **directly against** this project's core principle that human judgment stays central,
rather than for it. The whole point of the system is a co-founder that pushes back with
independently-grounded knowledge; a version that asks permission before disagreeing is a
mirror, which is the failure this project is built to avoid.

So: propose-then-confirm on writes, always (bar the ingestion exception). Zero gating on
disagreement in conversation, ever.

---

## 8. Devil's-advocate pushback design

When Claude pushes back on a proposal or surfaces a conflict, it does **not** hand down a
single verdict. It presents **at least two named, genuinely-argued stances** — a case-for
and a case-against, each argued in good faith on its own terms — and leaves the judgment to
the human.

How the stances are produced depends on stakes:

- **High-stakes** — a reconciliation that would overturn something already in the wiki, a
  trust-tag change, or a genuine contradiction. Here the stances are formed by **separate
  subagents that do not see each other's conclusion while forming it.** Each argues its
  side independently; neither is anchored to the other's reasoning. Only after both are
  formed are they presented together to the human.
- **Low-stakes** — an ad-hoc filing, a minor addition. Here Claude argues both stances
  **inline, no subagents.** Spinning up independent subagents for a small addition would
  manufacture confirmation-fatigue ceremony out of proportion to the decision.

**Why this design.** Independently-argued, AI-generated pushback is the primary defense
against automation bias — and the counterintuitive research finding is that AI pushback
measurably *increases* human deference rather than provoking harder thinking, unless it is
deliberately structured to force genuine consideration of more than one side. Presenting
two independently-argued stances, rather than one verdict the human can rubber-stamp, is
what keeps the human actually thinking.

This design is doubly source-grounded: it converges the reference material's own
thought-partner guidance (use a devil's advocate; use debating sub-agents) *and* the
reference material's independent sycophancy warning, with this project's own automation-bias
research finding. Three separate lines arriving at the same structure.

The **"grill me" interrogation skill** (future feature, out of scope here) plugs into the
high-stakes path as the mechanism for interrogating the human during reconciliation. Note
the plug point; do not build it here.

---

## 9. Reconciliation

Reconciliation is the manually-triggered (§1) process of resolving new information against
what the wiki already holds — updating, correcting, or overturning existing pages.

- Reconciliation writes are **gated by propose-then-confirm** (§7): they are wiki writes,
  not conversation, so they wait for confirmation.
- Reconciliation that overturns existing content, changes a trust tag, or resolves a
  contradiction is **high-stakes** and uses the **independent-subagent devil's-advocate
  path** (§8).
- The **"grill me" skill** plugs in here as well, as the interrogation front-end that
  surfaces and pressure-tests the human's position before a reconciliation is finalized.

---

## Quick reference

| Action | Gated by confirm? | Notes |
| --- | --- | --- |
| Deep-ingestion pass | **No** (the one exception) | Ends with mandatory self-verification (§4) |
| Create/edit a page | Yes | Default to edit over new (§3.1) |
| File an ad-hoc answer into the wiki | Yes | |
| Reconciliation update | Yes | High-stakes → independent subagents (§8, §9) |
| Conversational disagreement / pushback | **Never gated** | Fires immediately (§7.2) |
| `ABOUT-ME.md` growth (via `interrogate-me`) | **No** | Structurally outside the wiki, never covered by §7 to begin with; still requires `interrogate-me`'s own completeness checkpoint (show the draft, confirm it's enough) before writing — see that skill's `references/about-me.md` |
| Knowledge-testing companion file (via `interrogate-me`) | **No** | Diagnostic content about Alfonso's own grasp of a topic, not a claim about the world — exempt from §2's minimum bar (see above); same completeness-checkpoint-then-silent-write pattern as `ABOUT-ME.md` — see `references/knowledge-testing.md` |

Standing rules: no automation on a timer (§1) · automemory disabled repo-locally (§1) ·
every page trust-tagged and externally cited (§2, §6, with one named exemption) ·
index-first, never load the whole wiki (§5) · relative markdown links only, no wikilinks
(§3.3) · every `paired_with` pairing must also be a real inline link (§3.2).
