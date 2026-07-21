# Second Brain & LLM Wiki — Extensive Source Summary

*A comprehensive, general-purpose extraction of everything covered across three source videos on building an AI second brain with Claude Code: "5 Levels of a Claude 2nd Brain," "Turning Claude into a Second Brain" (the Claude Fable / AI Operating System video), and the video covering Andrej Karpathy's LLM Wiki method. Organized by topic rather than by source, since all three cover overlapping ground and build on each other. This is general knowledge about the pattern itself — not tied to any specific person's implementation.*

---

## 1. What a second brain is, and the problem it solves

A second brain is a persistent, external store of knowledge that an AI agent can read from and write to, so that talking to the AI compounds over time instead of resetting every conversation.

The core problem: normal AI chats are **ephemeral** — the knowledge built up in a conversation disappears once it ends. Without a system to capture it, every new conversation starts from zero, forcing constant re-explanation of the same background, decisions, and context. This method turns that repeated knowledge into something that compounds like interest in a bank, rather than evaporating.

At the most basic level, a second brain is just **markdown files organized in folders** — nothing more exotic is required to get real value. No database, no vector store, no complex infrastructure. The mental shift required is treating the AI less like a series of disconnected tool sessions and more like a colleague who accumulates real, permanent knowledge of you and your business over time — closer to a co-founder than a stranger you re-brief every time.

**Definition of the job of a second brain:** a place to save notes, meeting recordings, message threads, and other raw information, structured so both you *and* your agent can reliably find it again later. The test isn't "did I save it" — it's "can I find it again, and can my agent find it again." If the answer is no, the folder architecture and routing aren't set up correctly.

**Key mindset: work backwards from how you'll use the data.** Before deciding how to store something, think about how it will be *queried* later — because how something will be retrieved determines how it should be stored in the first place. (Analogy used: you wouldn't design a square ball because it needs to fit through a round hoop — the shape of retrieval determines the shape of storage.)

---

## 2. Second Brain vs. AI Operating System — the Four C's

A consistent two-layer model is used across the source material:

- **Second Brain = knowledge.** Does the AI actually know what's going on in your business, your life, your relationships? Can you ask it questions and get real, accurate answers?
- **AI Operating System (AIOS) = action.** Once the knowledge layer exists, you build automation, skills, and agents on top of it that actually *do* things — this can't exist without the second brain underneath it.

This breaks into a four-part framework, taken in strict order — **the first two constitute the second brain; the second two constitute the operating system layer built on top of it:**

1. **Context** — who you are, who your business is, static/evergreen background. This is the actual substance of the second brain.
2. **Connections** — the ability to reach *live* data (message threads, financial dashboards, project management tools) rather than storing static snapshots of things that constantly change. Static background goes in the brain directly; volatile data should be *reachable*, not duplicated.
3. **Capabilities** — skills, agents, automations, and pipelines built once context and connections exist.
4. **Cadence** — capabilities running autonomously on their own (on a schedule or trigger) without being manually triggered and babysat each time. This is explicitly the *last* thing to build, and has to be earned through demonstrated reliability — not started with.

**An OS doesn't start with architecture — it starts with a default.** The foundational mindset shift is defaulting to working inside the AI coding agent (rather than juggling separate tool tabs, custom GPTs, or one-off subscriptions) so that context, memory, and preference all accumulate in one place over time.

**The gut-check test:** if you asked your AI something about yourself or your business right now, would the answer sound like it came from a stranger, or from a teammate/co-founder who already knows what's going on?

---

## 3. The Five Levels of second brain maturity

A maturity ladder describing how the underlying knowledge is structured and retrieved. **Critical framing: higher levels are not "better."** The right level is whichever is the *simplest one that actually solves a real, felt pain point* — not the most sophisticated one available. Different sections of the same second brain can legitimately sit at different levels simultaneously (e.g., one folder might be level 2 while another is level 4).

Each level answers a different underlying question:

### Level 1 — Exact match / router
**Question: can you find a file by an exact word or filename?**
A single router file (e.g., `CLAUDE.md`, or `AGENTS.md` for other harnesses) is loaded automatically at the start of every session — functioning like a system prompt for that project. It contains routing rules: pointers to where different kinds of information live ("if you need info about me personally, look in this folder"). Alongside it: a handful of plain folders — commonly `context/` (always-true background, an "about me" file, a decision log), and `projects/` (ongoing ventures/clients, optionally organized by date).

If an AI agent ever asks "can you give me more info, I don't know what you mean" despite the relevant files existing somewhere in the project, that's a direct symptom of missing routing — the agent won't search an entire project automatically (and you wouldn't want it to, since that wastes time and tokens). When routing is set up properly, you stop having to re-explain things — the agent already knows where to look and why.

**Failure mode as this level grows:** it can get messy and start to feel like things are being "lost" or ignored, since retrieval is essentially exact keyword/filename matching.

**Important note:** there is *no single proven "correct" way* to organize a level-1 (or any level) second brain beyond a few common conventions (a router file, a context folder, a decisions log). Don't treat any one person's specific structure as the one right answer — what matters is whether the routing is intuitive to *you* and actually works for *your* agent.

### Level 2 — LLM Wiki (interlinked markdown)
**Question: can you pull everything related to a topic together?**
Files grow in number and start to take a different shape — organized into a wiki of interlinked markdown pages rather than flat files. Especially useful once there are 30+ notes and it's getting hard to remember what's in them. This is where the Karpathy method (detailed in section 4) lives.

This level also introduces **automemory** and a **memory file** — Claude Code can be told to automatically maintain and update a memory file on its own (toggle via `/memory`), so the model incrementally builds and revises its own notes without manual intervention for that specific file. For tool-agnosticism across harnesses (e.g. moving from Claude Code to Codex), the router file gets duplicated (`CLAUDE.md` copied to `AGENTS.md`, kept in sync), and the *other* harness is simply told where the memory file lives via routing — the memory mechanism itself doesn't need to be rebuilt per tool.

**Important distinction: wiki links are not the same as a true knowledge graph.** A wiki's backlinks are similar to "this page is referenced by that page" — but they don't carry *meaning* about the relationship (e.g., "endorsed by," "competitor of"). It's closer to following a trail and reading full pages in sequence than to querying explicit relationship semantics. One source explicitly states his entire real-world system sits at this level and he hasn't felt a strong enough pain point to move beyond it.

### Level 3 — Semantic / vector search
**Question: can you search using different words than what was literally written (search by meaning, not exact match)?**
This is where actual vector databases and embeddings enter the picture (Pinecone, Supabase, or similar). A document is chunked, and each chunk is run through an embeddings model that places it in a meaning-based multidimensional space — similar chunks cluster near each other. Retrieval works by searching for chunks *semantically similar* to a query, not by exact word match.

**Significant, commonly misunderstood limitation:** vector search retrieves *chunks*, not full documents. This means a query like "summarize the meeting from March 5th" might only pull back the 5 most semantically-similar chunks out of, say, 20 total chunks from that document — and can silently miss important information contained in chunks that didn't score as similar to the query wording, even though they were part of the same source. A vector database is not a magic solution that always retrieves everything relevant — it's genuinely good at finding *a specific, narrow answer* buried in a huge volume of largely irrelevant text (e.g., "what was rule #17 out of 1,000 rules"), but poor at tasks requiring *complete* context about one thing, where reading a whole markdown file directly and summarizing it will be more accurate than assembling an answer from disconnected retrieved chunks.

**Practical implication:** a second brain doesn't need to be uniformly one style. It's entirely reasonable for most of a project (context, decisions, projects) to remain plain markdown while one specific, high-volume, narrowly-queried subset (e.g., a large transcript archive) uses vector retrieval instead. The choice of markdown-vs-semantic-search for any given chunk of data should be made deliberately based on how that specific data will be queried, not applied uniformly across the whole system.

### Level 4 — Knowledge graphs
**Question: can you trace relationship chains — following a topic back through how it connects to other topics?**
Explicit entities (people, companies, tools, concepts) and explicit, named relationships between them (e.g., "Person X works at Company Y," "Company Y is a competitor of Company Z," "Tool A builds on Tool B"). This is generally the most complex and (depending on platform) the most expensive tier to run.

One source is explicit that he experiments with knowledge graphs but does *not* run his own day-to-day system on one, because routing files and a wiki have adequately met his needs — but he also notes his work is heavily project/content-based rather than involving a large CRM with many businesses/clients, and that a knowledge graph likely *would* make more sense for someone managing that kind of relationship-dense data.

**Feeding a knowledge graph with enough real data is often the actual bottleneck**, not the graphing technology itself (most knowledge-graph software handles the embedding/relationship-building automatically once given sufficient data — the hard part is getting enough detailed information out of a person's head and into the system in the first place). This is precisely the use case for the **"grill me" skill** (see section 6): interrogating a person relentlessly and specifically about a topic (a client, a business, a relationship) until enough has been extracted to actually populate meaningful relationships, rather than trying to write it all manually.

**Comparative tradeoff vs. a wiki:** a knowledge graph can be more lightweight at query time in one specific sense — a wiki-style system generally has to read an entire relevant page in full even if it only needed one small fact from it, whereas a graph can retrieve just the specific relationship/fact needed without pulling in a whole document.

**Important disclosure flagged in the source material:** anything processed through Claude (or any closed-source hosted model) is sent to that provider (Anthropic, in Claude's case) — this is explicitly called out as a real consideration for anyone who might be tempted to feed sensitive business or especially *client* data into a system built this way. For genuinely sensitive/private data, local/open-source models may be the more appropriate choice instead of a system routed entirely through a closed, hosted model.

### Level 5 — Always-on autonomous "brain OS"
**Question: has the whole system become fully autonomous, syncing and refreshing on its own without you thinking about it?**
Referred to in the source material by the example of "GBrain" (a concept associated with Y Combinator's Garry Tan, paired with something called "GStack") — everything from the earlier levels (wikis, routing, relationships, tools), but with constant, automatic syncing and memory refresh rather than manual, deliberate ingestion steps.

**Explicitly flagged risk, stated directly by the source material's own creator:** he does *not* run his personal system at this level, and names a genuine, unresolved concern: at some point, *more* context can stop helping and start actively hurting output quality — not just costing more tokens, but degrading the AI's actual reasoning. He frames this as a real dilemma, not something he's confidently solved — "when do you have too much context, and when does it get to the point where it's actually doing more damage than good."

### How to identify what level you actually need (diagnostic heuristics from the source material)
- Constantly re-explaining your setup, or need exact filenames/words to find things — **Level 1.**
- 30+ notes, increasingly hard to remember what's in them — **Level 2** (ingest into a wiki with relationships).
- Notes exist but searches using different wording than what was written keep missing them, and routing genuinely isn't working — **Level 3** (semantic search).
- Need to trace chains of relationships and follow connected threads of reasoning across many entities — **Level 4** (knowledge graph).
- Running multiple autonomous agents that need to stay synced with minimal manual intervention — **Level 5.**
- **If there's no actual pain point currently being felt, there's no need to build toward a more complex level "just in case."**

---

## 4. Karpathy's LLM Wiki method (the concrete reference implementation of Level 2)

This is a specific, simple, non-technical method that went viral (originally described by Andrej Karpathy) for building a level-2 second brain in a matter of minutes, requiring no fancy infrastructure.

**The three-part structure:**
- **`raw/`** — unprocessed source material dropped in exactly as received (an article, a transcript, a PDF's contents, etc.), never edited by hand.
- **`wiki/`** — the organized output. The AI agent reads what's in `raw/` and organizes it into a set of interlinked markdown pages, deciding on its own how to chunk, structure, and cross-reference the material — the person does not need to pre-design a taxonomy or folder scheme.
- **`log`** — the operation history: a running record of what's been ingested and when.

Within `wiki/`, an **index** file catalogs everything (an entry per page, organized by category — tools, techniques, concepts, sources, people, comparisons, etc., depending on the project). The index is what an agent reads *first* when answering a question, before deciding which specific pages are actually worth opening in full — this index-first approach is what keeps token usage low even as the wiki grows.

**A router file (`CLAUDE.md` or equivalent) is still required** to explain how the project works: where the wiki path is, how to search through it, how to update it, and (per the guidance in the source material) explicit instruction on *when not to bother reading the wiki at all* for a given request, to avoid wasting tokens on lookups that aren't actually needed.

**Setup process described (achievable in roughly 5 minutes):**
1. Create a project folder.
2. Open an AI coding agent (Claude Code or equivalent) pointed at that folder.
3. Provide Karpathy's original idea/prompt (deliberately left vague/general by its author so it can be adapted per-project) directly to the agent, along with an instruction establishing it as "my LLM wiki agent — implement this as my second brain, guide me step by step, create the CLAUDE.md schema," etc.
4. The agent creates the initial folder structure. By default, it may create subfolders like `analysis/`, `concepts/`, `entities/`, and `sources/` — but this isn't fixed; the actual organizational scheme should be discussed and adjusted with the agent as real content starts populating it. Karpathy's own guidance is explicit that sometimes a flat structure with no subfolders at all is preferable, and other times subfolders genuinely help — there's no single correct answer, and it depends on the nature of the content.
5. Drop a first real source into `raw/` and tell the agent to ingest it. The agent may ask clarifying questions first (what to emphasize, how granular to be, what the overall purpose of this specific vault/project is) — giving thorough answers to these upfront meaningfully shapes ingestion quality going forward, and it helps to explicitly state the *purpose* of the whole project (e.g., "this is specifically for my second brain, for personal/business things" vs. "this is purely a research project") so future ingestion is contextually appropriate.
6. The agent reads the source and writes new wiki pages — potentially producing many pages from a single rich source (example given: roughly 25 wiki pages generated from one long article). This can take real time for large sources (example given: ~10 minutes for one long article; ~14 minutes to batch-ingest 36 video transcripts, producing 23 wiki pages).

**Obsidian's actual role:** Obsidian is a free, optional tool that provides a *visual* layer (including a graph view) over the exact same underlying markdown files — it is not required infrastructure, and the system works identically without it. One source states he "hardly ever" opens Obsidian himself despite having it configured, specifically because he trusts that the underlying files and agent already handle retrieval correctly without needing the visual layer. If desired, a browser extension ("Obsidian Web Clipper") can pull web content directly into the `raw/` folder.

**"Hot cache":** a small, separate file (on the order of a few hundred words/characters) holding a compressed summary of the most recent relevant exchange or update — described specifically as useful in a *personal/business* second brain (where "what did we just discuss" recall matters) but explicitly *not* used in a more static, reference-style wiki (e.g., a video-transcript knowledge base), where that kind of "most recent thing" recall isn't a meaningful concept. This is a deliberate, contextual addition — not a universal requirement of the method.

**Linting / health checks:** Karpathy's own described practice is to run periodic "LLM health checks" over the wiki — looking for inconsistent data, filling in missing data via independent web research, and identifying interesting new connections or candidate topics/articles worth adding. This is framed as routine maintenance, run as often as desired (daily, weekly, on-demand), not a one-time setup step.

**Does this replace semantic search / RAG?** The source material's own answer: "no, but kind of yes," depending on the project's actual scale and goals. Advantages of the raw/wiki approach over classic vector-based RAG: it finds information by reading indexes and following links, which preserves *relationship* meaning (rather than just similarity scores); infrastructure cost is effectively zero beyond token usage (no embedding model, no vector database, no chunking pipeline to maintain); and maintenance is just periodic linting rather than needing to re-embed content whenever things change. The genuine limitation: this approach doesn't scale to enterprise-level volumes (millions of documents) the way a dedicated vector/RAG pipeline does — at that scale, traditional retrieval infrastructure becomes necessary. At the scale of hundreds of pages (the range explicitly cited as where this method holds up well), the wiki approach is described as both cheaper and more accurate.

---

## 5. Ingestion, growth, and maintenance mechanics

- **You are in control of what gets ingested** — sources are not passively vacuumed in; a person actively decides to hand something over ("here's my meeting transcripts from this week, help me think through this and let's ingest it together").
- Distinguish two categories of data explicitly: **context** (evergreen — still true and relevant a year from now, worth keeping permanently) vs. **connections** (fast-changing — message threads, current customer/deal data — this kind of data should be *reachable* live rather than dumped into static files that immediately start going stale and require ongoing manual cleanup).
- A concrete illustration of how "connections" work in practice: a vague question like "what did we talk about with a specific person last week regarding a specific topic" can be answered by the agent checking a relevant static file first, then the wiki, and finally reaching into a live connected tool (a project management platform, in the example given) if the answer isn't found in the static layers — this layered lookup, in the correct order, is itself what makes the system function as a genuine second brain rather than just a static archive.

---

## 6. Grill Me — the interrogation/extraction technique

A specific, named, reusable method: a skill that interviews a person relentlessly about a given topic — described examples range from roughly 15 to 30+ questions in a single session — continuing until the model judges it has extracted enough. It can also be fed supporting files (transcripts, contracts, documents) during the interrogation, not just verbal answers. Output is written into a dedicated "brainstorm" file/folder.

This is explicitly framed as a general-purpose knowledge-extraction tool, usable for: initial business/personal background, a specific client or relationship, a specific business idea, or — as an entirely separate later use — for reconciling real-world feedback back into the wiki when something learned in practice diverges from what's currently written down.

The underlying premise for why this matters: the actual bottleneck in building a good second brain is often not "the AI isn't retrieving things well" — it's "not enough has actually been extracted out of the person's head and into the system yet." Before concluding retrieval is failing, the more useful question is whether the folders/files genuinely hold the full nuance a person actually has in their head, or whether there's simply a gap in what's been captured at all.

---

## 7. Skills, capabilities, and delegation patterns

- **Skills don't need to be elaborate multi-step workflows** — a frequently-repeated prompt, turned into a reusable skill, counts. If the same request or workflow keeps recurring, that's the signal to formalize it as a skill.
- **Skills are treated as permanently unfinished, iterative artifacts.** Every time a skill is used, that use generates feedback — what worked, what didn't — and the skill should be explicitly updated afterward. A skill built months ago should still be actively revised on an ongoing basis as preferences, models, or requirements shift; there's no such thing as a "finished" skill.
- **"One AI doing one thing well" (assembly-line pattern).** Rather than doing everything in a single long session (risking degraded output quality as context fills up — referred to as "context rot"), work is deliberately broken into phases handled by separate, specialized sessions/agents: research happens in one focused pass, its output feeds a drafting pass, which feeds a polishing pass, with a context-clearing step between phases. Each specialized step gets a clean, focused context rather than one session accumulating everything.
- **Delegation for parallel work, distinct from the phase-based approach above:** for tasks that can run simultaneously rather than in sequence, work can be delegated out to cheaper/faster models for the individual sub-tasks, with a single higher-capability model consolidating the results into one clean summary at the end — useful specifically when using a more expensive top-tier model, to control cost.
- **CLI/API access is generally preferred by the source material's creator over MCP servers** for connecting to external tools, citing a feeling of greater control and generally lower cost — though MCP remains a valid option depending on preference. The stated approach to setting up a new connection: search for the target service's API documentation, hand that research to the coding agent (or have the agent do the lookup itself), and have it identify exactly which endpoints are needed.

---

## 8. Cadence, automation, and the permission-layer principle

Automation is explicitly the *last* layer to build, and has to be *earned* — not something to set up preemptively just because the underlying knowledge and skills exist. Two real costs are named as increasing together as more autonomy is introduced: **cost** (more AI usage) and **risk** (more that can go wrong unsupervised). A third, easily overlooked cost: **ongoing maintenance** — putting something into an automated, unattended state does not mean it can be forgotten about; it still needs periodic visibility and check-ins to confirm it's actually still working correctly and still adding value, and someone still needs clear ownership over it.

**Ways automation can be triggered**, as distinct categories: manually (on request only), by an event (e.g., a new email or a new booking), or on a schedule (e.g., every Monday). **Ways it can be deployed**, as distinct implementation options: as routines/loops within the coding agent itself, as separate deterministic scripts, or as workflows pushed into a dedicated automation platform.

**The central governing principle: "a prompt is never a permission layer."** The correct operating assumption for any agent with real access to a real system: *if it can do something, at some point it will* — whether or not that specific action was ever explicitly requested. Access should be scoped through actual technical permissions/credentials, not through instructions alone (e.g., a deliberately scoped API key limited to *only* reading meeting transcripts, with no ability to edit or delete, is a real permission layer — a written instruction not to edit or delete is not).

**The illustrative incident described in the source material:** an autonomous agent, while working through a task list, misinterpreted an instruction and sent an incorrect discount code to an email list of roughly 150,000–200,000 people, requiring a public apology. The framing given for how this was handled afterward is notable: it was treated as valuable data and a case study for the whole team to learn from, not as a reason to assign individual blame — the actual fix was tightening what the agent technically had the *keys* to do going forward, not simply resolving to "trust it less" in the abstract. The broader principle drawn from this: every mistake made by the system, including outright failures, should be treated as data that improves the system going forward (fix the underlying instruction/permission so the same failure mode can't recur), rather than treated purely as a failure to feel bad about.

---

## 9. Using the AI as a thought partner (usage discipline, not architecture)

Several practical usage habits are described as directly affecting how much real value the second brain actually delivers, independent of its technical structure:

- **Treat it as a thought partner to brainstorm and be challenged by — not an oracle to be handed decisions.** Get a response, then push back on it and have it push back in return, rather than accepting a first answer and immediately acting on it.
- **Models have a natural tendency toward sycophancy** — a documented general tendency to agree with and please the person they're talking to, described as an acknowledged, industry-wide issue with AI models generally (with some indication of gradual improvement over time, but not something to assume is solved). Actively correct for this rather than assuming any given response reflects genuine, independent pushback by default.
- **A concrete technique for counteracting this:** deliberately have the AI spin up multiple sub-agents or distinct personas to argue *different* perspectives or take different sides of an issue, rather than relying on a single synthesized response — using the resulting spread of viewpoints to inform a final human judgment call, rather than treating any single AI response as the answer.
- **Use the grill-me technique on the system itself, not just business content** — one example given is using it to help work out and document the reasoning behind the second brain's own design and usage patterns, not solely external business knowledge.
- **Verify the work before trusting it.** Whatever the AI produces should be checked — using whatever method of verification is appropriate to the type of output (visual inspection, automated browser-based testing/clicking through a UI, checking outputs against different plausible "personas" or use cases) — rather than accepted at face value on a first pass. Explicitly framed as a genuine quality-difference driver: without a verification step, output often lands at a rough, partially-complete state requiring several rounds of manual correction; with a self-verification step built in, initial output tends to already be much closer to final/correct, still generally benefiting from some iteration but starting from a meaningfully stronger baseline.
- **Explicitly instruct the AI to cite its actual source** when it states a fact ("show me the exact source where you're getting this data from") — this is named as one of the more effective ways to catch and correct instances where the model confidently states something incorrect, since it will do so with the same confident tone whether right or wrong.

---

## 10. Tool-agnosticism as a design principle

A repeatedly emphasized principle: the actual system being built — the second brain and its accompanying operating system — is fundamentally just folders, markdown files, skills, and routing logic. It is explicitly **not** meant to be thought of as "a Claude Code second brain" or tied permanently to any single AI product or model. Because the substance lives in plain files, switching the underlying AI harness or model (e.g., between Claude Code and Codex, or as new model versions are released) does not require rebuilding anything — only pointing a different tool at the same folder, and maintaining a parallel router file per harness where needed (`CLAUDE.md` alongside `AGENTS.md`). This is framed as removing a significant source of anxiety about tool/model churn: the underlying knowledge and capability being built is a durable, personal asset independent of whichever specific AI product happens to be reading it at any given time.

---

## 11. Practical / FAQ-style points from the source material

- **Do you need to know how to code to start?** No — starting from a genuinely empty folder and having the coding agent itself walk through initial setup is explicitly presented as sufficient; no pre-existing technical skill is treated as a prerequisite.
- **What happens when the AI confidently states something wrong?** As soon as an error is caught, the fix should be written back into the system immediately — updating the router file and/or the relevant skill so the same specific mistake doesn't recur — rather than just correcting it verbally in the moment and moving on.
- **What if the system is left unused for a stretch of time (e.g., several weeks)?** Framed as low-risk on its own — mainly just requiring a re-sync or catch-up ingestion of anything that happened during the gap, not something that meaningfully "breaks" from disuse.
- **Team/shared versions of a second brain:** framed as something each individual should build and understand personally first, before attempting to roll it out to others — both to be able to actually teach it, and because the harder problem in a team setting isn't the technology choice (which specific tool holds shared knowledge) but *adoption*: getting the people who own a given piece of information to actually keep their part of the shared system updated, and getting others to actually consult and reuse existing knowledge rather than continuing to just ask the same people the same questions repeatedly, which duplicates both knowledge and effort across a team.
- **Cost note:** an early/frontier top-tier model can consume a subscription's usage allowance considerably faster than a mid-tier model when used for this kind of knowledge-heavy work — worth being aware of as a practical constraint if using a top-of-line model for heavy second-brain work specifically, though costs and specific figures shift over time and shouldn't be treated as fixed facts.
