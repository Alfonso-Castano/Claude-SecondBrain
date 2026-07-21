---
title: Skills, Capabilities, and Delegation Patterns
folder: shared
tags: [second-brain, skills, delegation, multi-agent, context-rot]
created: 2026-07-21
last_updated: 2026-07-21
source: raw/2026-07-21-second-brain-transcripts-full-summary.md
confidence: extracted
---

## Skills don't need to be elaborate

Skills don't need to be elaborate multi-step workflows — a frequently-repeated prompt, turned into a reusable skill, counts. If the same request or workflow keeps recurring, that's the signal to formalize it as a skill, not a signal that it needs to be architected as something bigger first.

## Skills are permanently unfinished

Skills are treated as permanently unfinished, iterative artifacts. Every time a skill is used, that use generates feedback — what worked, what didn't — and the skill should be explicitly updated afterward. A skill built months ago should still be actively revised on an ongoing basis as preferences, models, or requirements shift. There's no such thing as a "finished" skill, and treating one as done after its first version is a way maintenance quietly stops happening.

## "One AI doing one thing well" (assembly-line pattern)

Rather than doing everything in a single long session — risking degraded output quality as context fills up (referred to directly in the source material as "context rot") — work is deliberately broken into phases handled by separate, specialized sessions/agents: research happens in one focused pass, its output feeds a drafting pass, which feeds a polishing pass, with a context-clearing step between phases. Each specialized step gets a clean, focused context rather than one session accumulating everything.

*(The "context rot" concern named here in passing is the same phenomenon independently and rigorously studied in the AI research literature — see [Context Rot — What the Research Actually Shows](../claude-knowledge/context-rot-research.md) for the actual data behind it.)*

**This directly matches how Alfonso already works.** Per `raw/2026-07-21-second-brain-for-me.md`, multi-chat workflows — one chat as a context-rich backend, another for focused output, with distilled context deliberately handed between them — are how this entire second-brain project was itself built (a working chat, a separate video-context chat, a business-foundation chat, and the build-phase agent). The assembly-line pattern described here isn't a hypothetical technique to consider adopting; it's already the operating mode, and the practical implication is that this second brain needs to stay **legible across handoffs** — context extractable and summarizable for a fresh session, not trapped in a way that only makes sense inside one continuous conversation.

## Delegation for parallel work

Distinct from the phase-based approach above: for tasks that can run simultaneously rather than in sequence, work can be delegated out to cheaper/faster models for the individual sub-tasks, with a single higher-capability model consolidating the results into one clean summary at the end. This is useful specifically when using a more expensive top-tier model, as a way to control cost while still getting parallel throughput.

## CLI/API access over MCP servers

The source material's creator states a general preference for CLI/API access over MCP servers when connecting to external tools, citing a feeling of greater control and generally lower cost — though MCP remains a valid option depending on preference. The stated approach to setting up a new connection: search for the target service's API documentation, hand that research to the coding agent (or have the agent do the lookup itself), and have it identify exactly which endpoints are needed.
