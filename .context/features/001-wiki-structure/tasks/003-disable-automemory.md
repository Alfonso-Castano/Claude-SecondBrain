# Task 003: Disable Claude Code automemory, scoped to this repo

**Status:** done
**Depends on:** none
**Model tier:** mid — the `update-config` skill supplies the mechanism, but the executor must actually invoke it, interpret its findings, and correctly scope the result to this repo rather than applying a guessed setting.

## Files
- Modify (exact path determined by the `update-config` skill — likely `.claude/settings.json` or `.claude/settings.local.json` at repo root; report whichever it actually is): the Claude Code settings file controlling automemory for this project.

## What to do

`OVERVIEW.md`'s constraints require: "Claude Code's automemory feature must be explicitly disabled — this needs to be a deliberate, stated setting in `CLAUDE-WIKI.md`, not something left to default behavior." Automemory writing without confirmation directly violates this project's propose-then-confirm principle.

Per `.context/DECISIONS.md` (2026-07-15 entry, "Automemory-disable mechanism: open item, needs verification"): a prior subagent lookup claimed the setting is `autoMemoryEnabled` in `.claude/settings.json`, with project-scoped settings taking precedence over the user-wide default — **but this claim is explicitly unverified** (flagged as resembling injected content, key and doc URLs not independently confirmed). Do not hand-apply that lead directly.

1. Invoke the `update-config` skill (via the Skill tool, `skill: "update-config"`) with the goal: verify the actual, current mechanism for disabling Claude Code's automemory feature, and apply it scoped to this repo only (must not change the setting for Alfonso's other Claude Code projects at the user level).
2. Let the skill determine and apply the correct setting/file/scope — do not override its findings with the unverified `autoMemoryEnabled` lead if the skill finds something different.
3. After the skill completes, confirm no automemory content is currently being written for this project (the DECISIONS.md entry notes none had been written as of project init — reconfirm that's still true, or note if it's changed).
4. In your completion report, state explicitly: the exact setting key/value applied, which file it lives in, and the confirmed scope (repo-local, not user-wide). This will be read verbatim by Task 005 (`CLAUDE-WIKI.md`) to write the "automemory is disabled" statement into the schema, and it must be accurate.

## Interfaces
- Consumes: `.context/DECISIONS.md`'s 2026-07-15 entry (the unverified lead and why it's unverified).
- Produces: the confirmed setting key/file/scope, stated in this task's own Evidence section after completion — Task 005 reads this task file directly to get that information (do not touch `.context/DECISIONS.md` yourself; superseding that entry is `/update-context`'s job, not this feature's).

## Constraints
- Do not edit `.context/DECISIONS.md` — per this project's file-ownership contract, only `/update-context` appends to it. Report your findings in this task's Evidence section instead; a future `/update-context` run will fold it in.
- Do not apply any automemory-related change at the user-level config (`~/.claude/settings.json` or equivalent) — scope must stay this repo only.
- If the skill's findings are ambiguous or it cannot fully verify a mechanism, report that plainly (BLOCKED) rather than guessing — this setting has already had one unverified lead recorded; don't add a second one.

## Verification
Run whatever check the `update-config` skill itself provides to confirm the setting is applied (e.g. re-reading the modified settings file and confirming the key/value is present, or the skill's own built-in verification step). State the exact command/check run and its output in Evidence.

## Evidence

`update-config` skill invoked; found `autoMemoryEnabled` documented in Claude Code's own bundled settings schema (independent of the earlier unverified subagent lead from initialization, though it corroborates the same key). Applied `{"autoMemoryEnabled": false}` to `.claude/settings.json` (repo-local, committable). Independently re-verified by the dispatching session (not just the executor's own report): file content confirmed via direct read to be exactly `{"autoMemoryEnabled": false}`; `~/.claude/settings.json` (user-level) confirmed to contain no `autoMemoryEnabled` key, i.e. unaffected; `git status --porcelain` confirmed only `.claude/` is new from this task. Scope: repo-local only, does not affect other Claude Code projects. Executor: sonnet, DONE.

**Confirmed setting for Task 005 to state:** Automemory is disabled for this repository via `autoMemoryEnabled: false` in the repo-local `.claude/settings.json` (committed, repo-scoped). Does not affect automemory in any other Claude Code project on this machine.
