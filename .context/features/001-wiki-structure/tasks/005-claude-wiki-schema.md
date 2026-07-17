# Task 005: Write CLAUDE-WIKI.md (full schema)

**Status:** done
**Depends on:** 002 (markdown tooling — need the exact `npm run` command names), 003 (automemory disable — need the confirmed setting to state)
**Model tier:** quality — this is the single most architecturally important document in the project (per `.context/research/SUMMARY.md`, the propose-then-confirm/pushback design is the project's most distinctive, least-precedented piece); every section below requires turning a settled decision into correctly-scoped operating prose, not just transcription.

## Files
- Create: `CLAUDE-WIKI.md` (project root)
- Read (do not modify): `.context/features/001-wiki-structure/tasks/003-disable-automemory.md` — read its Evidence section for the exact automemory setting key/file/scope to state in this document.

## What to do

Write `CLAUDE-WIKI.md` at project root — the dedicated schema file governing all wiki operating rules. `CLAUDE.md` (Task 006) will point to this file rather than containing these rules itself. Section ordering/internal structure is your judgment to make (`CONTEXT.md`'s Open Questions explicitly leaves this open) — the content below is exhaustive and must all be present in some coherent form. Every decision below is already settled (from `CONTEXT.md`'s Implementation Decisions and `OVERVIEW.md`'s Constraints) — your job is correct, complete, unambiguous prose, not re-deciding anything.

Required content:

**1. Frontmatter template.** Every wiki page (`wiki/shared/` or `wiki/claude-knowledge/`) requires YAML frontmatter with these fields: `title`, `folder` (`shared`|`claude-knowledge`), `tags`, `created`, `last_updated`, `source`, `confidence` (`extracted`|`inferred`|`ambiguous`), `paired_with` (omitted entirely if the page is unpaired — not left blank/null). State that no page may exist without, at minimum, a trust tag (`confidence`) and a citation (`source`) that bottoms out outside the wiki.

**2. New-page-vs-edit rule.** Default toward merge/edit over creating a new page, per Zettelkasten's atomic-note discipline. A new page is warranted only for something that's a genuinely distinct entity/concept worth linking to from elsewhere — not a reflex for every new fact.

**3. `shared`/`claude-knowledge` pairing — earned, not mechanical.** Never create a stub on the other side of a pairing just to satisfy the convention. Name the failure mode this avoids: low-information stub files diluting the index (the closest analogous pattern, Zettelkasten literature-notes vs. permanent-notes, has this exact documented failure mode).

**4. Anti-wikilink rule.** Standard relative markdown links only (`[Topic](../claude-knowledge/topic.md)`), never `[[wikilink]]` syntax — state plainly that no resolver exists for it since Obsidian is deferred, and that this needs to be stated explicitly because wikilink syntax is a plausible default from general PKM training data.

**5. Ingestion workflow.** Describe the deep-ingestion pass: the one path that writes directly to the wiki without per-page confirmation (handing over a source is itself an act of trust). Must include, as a distinct closing step (not folded into trust-tagging): **self-verification** — after a deep-ingestion batch, Claude checks its own ingestion batch for accuracy before considering the pass complete. State explicitly that this is separate from trust tags: trust tags describe confidence in a claim, self-verification is Claude actually checking its own work, and given deep ingestion writes with zero per-page human review, this is the pass's own closing step, not optional polish.

**6. Query workflow.** Index-first discipline: read `index.md` (project root) first, drill into only relevant pages, never load the whole wiki into context. Trust-tag enforcement: the trust tag must be surfaced whenever a claim is cited back in conversation — not only when the source page itself is opened.

**7. Lint workflow.** Must include all of:
   - `npx markdownlint-cli2` + `npx markdown-link-check` (via `npm run lint:md`, `npm run lint:links`, or `npm run lint` — the exact script names set up in `package.json` by this feature) as the deterministic, non-AI first step of every lint pass.
   - Orphan-page detection.
   - Index-entry-vs-page-content drift detection.
   - Citation-chain-bottoms-out-externally check: every `claude-knowledge` page's citation must trace outside the wiki (a raw file, external research, or a dated conversation) — never to another wiki page.
   - `index.md` size/token trigger: flag at ~150–200 entries or ~3–4k tokens.
   - Trust-tag enforcement (cross-reference with query workflow's requirement).
   - **Proactive gap-surfacing:** lint isn't only hygiene — it must also proactively surface gaps and "interesting connections for new article candidates," i.e. suggest what's worth researching or ingesting next, not just fix what already exists.

**8. Propose-then-confirm rule, with the write-only-gating boundary stated explicitly.** Propose-then-confirm governs every wiki *write* (creating or editing a page, filing an ad-hoc conversational answer, a reconciliation update) except the one named deep-ingestion exception (§5). State this boundary as its own clearly-labeled point, not buried in a sentence: **this gate applies to writes only — it must never gate conversational pushback or disagreement, which fires immediately and un-gated.** Explain why this matters: if confirm-gating (which only exists to govern what gets written) bleeds into how readily Claude voices disagreement in conversation, that works directly against this project's core principle rather than for it.

**9. Devil's-advocate pushback design.** Pushback proposals present at least two named, genuinely-argued stances (case-for / case-against) instead of a single verdict. Differentiate by stakes:
   - **High-stakes** (reconciliation overturning something already in the wiki, a trust-tag change, a contradiction): the stances are formed by **separate subagents that don't see each other's conclusion while forming it**.
   - **Low-stakes** (ad-hoc filing, minor additions): done inline by Claude, no subagents — avoids confirmation-fatigue ceremony on small things.
   State the rationale: this is the primary defense against automation bias (independently-researched AI pushback measurably *increases* human deference rather than provoking harder thinking), and it's doubly source-grounded — the reference material's own thought-partner guidance (devil's advocate, debating sub-agents) plus its independent sycophancy warning, converging with this project's own automation-bias research finding.

**10. Automemory.** State, as a deliberate, explicit setting (not left to default behavior): Claude Code's automemory feature is disabled for this repo. Read `.context/features/001-wiki-structure/tasks/003-disable-automemory.md`'s Evidence section and state the *actual* confirmed setting key, the file it lives in, and the scope (repo-local) — do not restate the unverified `autoMemoryEnabled` lead from `.context/DECISIONS.md`'s 2026-07-15 entry if Task 003 found something different.

**11. No automation on a timer.** State plainly, as a standing rule covering ingestion, lint, and reconciliation alike: nothing in this system runs on a schedule, ever — every workflow is manually triggered, permanently, not just at initial launch.

You may reference the "grill me" interrogation skill as a dependency of ingestion/reconciliation workflows without it existing yet (it's explicitly out of scope for this feature, deferred to its own future feature) — don't design around its absence, just note where it plugs in.

## Interfaces
- Consumes: exact `npm run` script names from Task 002's `package.json` (`lint:md`, `lint:links`, `lint`); the confirmed automemory setting from Task 003's Evidence.
- Produces: `CLAUDE-WIKI.md` at the exact path Task 006's `CLAUDE.md` router points to.

## Constraints
- Do not build the "grill me" skill itself — reference it as a dependency only.
- Do not write any actual wiki pages, index entries, or log entries as part of writing this schema — this task only produces the schema document itself.
- Do not re-decide anything listed above — every item is already settled; if something here seems to conflict with the project's human-judgment-stays-central principle, stop and flag it rather than resolving it silently (per `CONTEXT.md`'s Global Constraints).

## Verification
Run:
```
cat CLAUDE-WIKI.md
```
Confirms manually: all 11 required content items above are present in some form, the write-only-gating boundary (item 8) is stated as its own explicit point rather than implied, and the automemory statement (item 10) names a real setting (not the unverified lead) sourced from Task 003's Evidence.

## Evidence

`CLAUDE-WIKI.md` created at project root, independently read in full by the dispatching session (not just the executor's own report) to verify all 11 required content items are present: frontmatter template (§2), new-page-vs-edit (§3.1), earned pairing (§3.2), anti-wikilink (§3.3), ingestion + self-verification (§4), query workflow (§5), lint workflow including proactive gap-surfacing (§6), propose-then-confirm with the write-only-gating boundary as its own labeled §7.2, devil's-advocate design (§8), automemory statement matching the confirmed setting exactly (§1), and no-automation-on-a-timer (§1). Executor: opus, DONE.
