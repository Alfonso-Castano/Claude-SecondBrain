# Decisions Log

Running record of decisions that constrain future work. Newest first. Any future session or skill should check here before re-deciding something already settled.

## 2026-07-15 — No standalone roadmap

**Decision:** No `.context/ROADMAP.md` was created.
**Rationale:** The project's full arc before steady-state feature-loop use reduces to two already-named, already-sequenced features fully specified in `OVERVIEW.md`'s Context section — build the wiki structure and `CLAUDE-WIKI.md` schema (Feature #1), then re-ingest the two already-held sources through it. This is ordinary `/feature` sequencing, not phase decomposition; a separate roadmap would only restate what `OVERVIEW.md` and `.context/research/SUMMARY.md` already say.
**Made during:** Project initialization

## 2026-07-15 — Schema file name and location

**Decision:** The dedicated schema file (governing ingestion/query/lint workflows, new-page-vs-edit rule, shared/claude-knowledge convention, propose-then-confirm) is `CLAUDE-WIKI.md` at the project root.
**Rationale:** Sibling to `CLAUDE.md`, keeps the router/detail split visible at a glance. Decided live during initialization rather than deferred to Feature #1's own discuss/plan loop, per Alfonso's preference.
**Made during:** Project initialization

## 2026-07-15 — Repo location confirmed

**Decision:** `Claude-SecondBrain` (this repo, at `c:\Users\alfon\SecondBrain\Claude-SecondBrain`) is the final home for the project.
**Rationale:** Confirmed settled by Alfonso at initialization, though explicitly open to change later if a real reason emerges — not treated as permanently locked.
**Made during:** Project initialization

## 2026-07-15 — Automemory-disable mechanism: open item, needs verification

**Decision:** Not yet decided. `build-handoff.md` requires Claude Code's built-in automemory feature be turned off for this project (it writes without confirmation, violating the propose-then-confirm principle). During initialization, an automemory instance was found actively writing session memory for this exact project at `~/.claude/projects/<project-id>/memory/`, outside this repo and untracked by the wiki's own log/citation/lint machinery.
A subagent lookup (claude-code-guide) reported that automemory is controlled by a project-scopable setting (`autoMemoryEnabled` in `.claude/settings.json`, with local/project settings taking precedence over the user-wide default) — meaning it could plausibly be disabled for this repo alone without affecting Alfonso's other Claude Code projects. **This claim is unverified** — the harness flagged the subagent's response as resembling injected instruction content, and neither the exact setting key nor the cited doc URLs were independently confirmed.
**Rationale for deferring:** No automemory content has actually been written from this session (verified — none was saved during this initialization). The fix should go through the `update-config` skill, which is built to configure `settings.json` correctly and can verify the real mechanism, rather than hand-applying an unverified JSON snippet.
**Next step:** Before or during Feature #1, use `update-config` to verify the actual disable mechanism and apply it scoped to this repo, then document the confirmed setting in `CLAUDE-WIKI.md`.
**Made during:** Project initialization

## 2026-07-15 — Research-surfaced gaps deferred to Feature #1, not resolved here

**Decision:** Concrete gaps found during domain research (page-level YAML frontmatter template, anti-`[[wikilink]]` rule, earned-not-mechanical `shared`/`claude-knowledge` pairing, a concrete lint checklist, stakes-differentiated propose-then-confirm, reconciliation requiring Alfonso's own counter-reasoning rather than accept/reject) are recorded in `.context/research/SUMMARY.md` for Feature #1's discuss/plan loop to pick up, not decided or written into `CLAUDE-WIKI.md` during this initialization.
**Rationale:** Per the project's standing principle, decisions this substantive about the wiki's actual operating rules stay human-reviewed through the full feature loop rather than being defaulted by an init script.
**Made during:** Project initialization
