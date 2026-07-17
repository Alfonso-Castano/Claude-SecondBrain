# Research: Feature #1 (Wiki Structure)

Scoped narrowly to the three items `CONTEXT.md`'s Open Questions flagged for research. Every other implementation decision in `CONTEXT.md` was already settled and is not re-litigated here.

## 1. Markdown tooling: `markdown-link-check` vs. `lychee`

**Decision: `markdown-link-check` (npm), not `lychee`.**

`CONTEXT.md`'s Implementation Decisions already commit to "`markdownlint-cli2` + a link-checker as real dev dependencies (`package.json`)" — a single-ecosystem, `npm install`-only setup with no separate binary/toolchain to manage, consistent with the project's no-build-pipeline, minimal-tooling-ceremony posture (`OVERVIEW.md`: "no separate frontend, no database," "no DB, server, or build pipeline needed" per `.context/research/SUMMARY.md`).

- `markdown-link-check` (`tcort/markdown-link-check`) is a genuine npm package — `npm install --save-dev markdown-link-check` is the entire install step, same as `markdownlint-cli2`. Confirmed actively maintained ("Sustainable" status, releases within the past 12 months, ~134k weekly downloads as of this research pass).
- `lychee` is faster and more feature-rich (async Rust, built-in wikilink resolution — irrelevant here since this project explicitly rejects `[[wikilink]]` syntax), but it is **not** an npm package. Distribution is via cargo/`cargo binstall`, prebuilt GitHub-release binaries, Docker, or OS package managers (Nix, Scoop, WinGet, Chocolatey, conda-forge) — a second install mechanism outside `package.json`, on a Windows dev machine specifically. A same-named `lychee` npm package exists but is an unrelated package, not a wrapper around the Rust tool.
- No source found directly benchmarks the two for a personal-wiki use case; the deciding factor is packaging fit, not raw speed, since this wiki will run link-checking on at most a few hundred pages manually-triggered — well within either tool's comfortable range.

**Conclusion:** `markdown-link-check` keeps the entire tooling surface inside one `package.json`/`npm install`, which is what "as real dev dependencies" was already signaling. `lychee` is the better link checker in the abstract but the wrong fit for this project's stated setup.

## 2. `log.md` format validation

**Decision: keep Alfonso's confirmed pipe-delimited, newest-first format as specified. Add one small, precedent-backed extension: a rotation trigger, stated in the header the same way `index.md`'s size trigger already is.**

Findings from the closest comparable implementations of Karpathy's raw/wiki pattern:

- Karpathy's own gist describes `log.md` as append-only and chronological, with the concrete guidance that "if each entry starts with a consistent prefix... the log becomes parseable with simple unix tools" (his own example: `## [2026-04-02] ingest | Article Title`, enabling `grep "^## \[" log.md | tail -5`). This validates the *shape* of Alfonso's proposal — a consistent, parseable, delimited prefix per line — even though the exact delimiter differs (his example uses a markdown-heading + bracket style; Alfonso's is flat pipe-delimited). Pipe-delimited is at least as grep/parse-friendly and is simpler to append/prepend by hand or by Claude, so there's no reason to switch.
- One concrete implementation (`Astro-Han/karpathy-llm-wiki`) rotates `log.md` to `log-YYYY.md` once it exceeds ~500 entries, checked during lint passes — directly analogous to the `index.md` size/token trigger already decided in `CONTEXT.md` (~150–200 entries or ~3–4k tokens). No source contradicts this; it's a small, cheap-now/expensive-later addition in the same spirit as the index trigger, so it's included in `log.md`'s seeded header as a stated future trigger, not built now (nothing to rotate yet — `raw/`/`wiki/`/`log.md` all start empty, consistent with `CONTEXT.md`'s explicit "no placeholder content" decision).
- **Genuine tension, called out rather than silently resolved:** the general append-only convention in comparable implementations appends chronologically (oldest-first, cheap — pure file append, `tail` gets the newest). Alfonso's confirmed format is newest-first, which requires prepending on every write (trivial for Claude to do, since it already rewrites files rather than shelling out to `>>`, but a real deviation from the "true append-only" pattern found elsewhere). This is a readability-vs-convention tradeoff, not a correctness issue — newest-first means the most recent activity is visible without scrolling, which matches how `log.md` is meant to be used (a human occasionally skimming recent operations, not a machine tailing a stream). Recommendation: keep newest-first as Alfonso already confirmed; note the tradeoff in the file's own header comment so a future reader understands why it deviates from the more common convention, rather than assuming it's an oversight.

**Conclusion:** `YYYY-MM-DD | <ingest|lint|reconcile|file> | <short description> | <files touched>`, newest-first, is validated as sound and is used as specified. Add a one-line rotation-trigger note to the seeded header (rotate to `log-YYYY.md` past ~500 entries, checked during lint) as a small, precedented, non-scope-expanding addition.

## 3. `ABOUT-ME.md`: single file vs. folder

**Decision: single file, `ABOUT-ME.md` at project root — resolved, not left open.**

No comparable second-brain/wiki implementation found uses a folder for personal/about-me context:

- Karpathy's own pattern has no dedicated personal-context file at all — personal knowledge (goals, health, self-improvement) is filed as ordinary wiki pages like anything else.
- The closest comparable implementation with an explicit personal-context layer (`coleam00/second-brain-starter`) uses **multiple distinct single-purpose root-level files** — `USER.md` (profile/accounts/preferences), `SOUL.md` (agent personality/values/boundaries), `MEMORY.md` (key decisions/lessons/active projects) — generated by a one-time `BOOTSTRAP.md` wizard. This is a split across *different concerns* (who-the-user-is vs. how-the-agent-behaves vs. what's-been-decided), not a decomposition of one "about me" concept into a folder of files.
- This project's `ABOUT-ME.md` is scoped to exactly one concern — "what Claude learns about Alfonso" — which is the direct analogue of `second-brain-starter`'s single `USER.md` file, not its three-file split (this project already has separate homes for the other concerns: `CLAUDE-WIKI.md` for operating rules, `.context/DECISIONS.md` for decisions, `wiki/` for domain knowledge). A folder would be introducing structure with no precedent and no found rationale — it would only make sense if `ABOUT-ME.md` needed to grow into multiple distinct concerns of its own, which nothing in `CONTEXT.md` or `OVERVIEW.md` calls for.

**Conclusion:** `ABOUT-ME.md`, single file, project root, sibling to `CLAUDE.md`/`CLAUDE-WIKI.md` — as `CONTEXT.md` already leaned, now confirmed by research rather than left open.

## What this changes in the task decomposition

- Task for markdown tooling: `package.json` + `markdownlint-cli2` + `markdown-link-check` as npm devDependencies, config files for both, no separate binary install step.
- Task for wiki scaffolding: `log.md`'s seeded header includes the pipe-delimited format spec plus the rotation-trigger note.
- `ABOUT-ME.md` is a single file task, no folder question left to resolve at execution time.
