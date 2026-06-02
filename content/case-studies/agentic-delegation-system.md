---
title: "Building an 8-layer agentic delegation system: orchestration, routing, and cost discipline across a multi-LLM stack"
date: 2025-09-12T14:00:00-05:00
draft: false
tags: ["case study", "AI infrastructure", "agentic systems", "multi-LLM", "automation"]
categories: ["case studies"]
description: "A completed agentic orchestration framework defining 8 delegation layers, 7 workflow types, a free-first routing matrix, and an inbox/outbox handoff protocol for multi-agent AI task execution — built as a standalone operating system for AI-assisted marketing work."
summary: "The Agentic Org Chart and Workflow System defines how AI tasks are structured, routed, and executed across a multi-provider stack (Witsy, Ollama, OpenRouter, Cerebras, Groq, Google, xAI). The framework separates strategy from execution, writer from critic, and establishes cost discipline rules that reserve premium model tokens for synthesis and QA — not bulk processing."
stat: "8"
statLabel: "Layer Agentic System"
statSubtitle: "Orchestration · Routing · Cost Discipline"
cover:
  image: "/makeoverlyonline/images/case-studies/agentic-delegation-system.jpg"
  alt: ""
  caption: ""
ShowToc: true
TocOpen: false
---

## The problem this solves

Running multiple AI models across multiple providers without a routing framework produces predictable outcomes: premium model tokens burned on low-value tasks, no separation between the agent doing the work and the agent checking it, no cost discipline, no status tracking between agents, and no systematic handoff protocol.

This framework solves all of it.

## The 8-layer hierarchy

Each layer has a defined ownership scope, specific inputs, and specific outputs. Nothing crosses layers informally.

**Layer 0 — Principal.** Human decision owner. All escalations terminate here.

**Layer 1 — Executive Orchestrators.** Set goals, define scope, assign workflows, approve escalations, accept final output on high-stakes tasks.

**Layer 2 — Delegation Managers / Routers.** Choose model and service. Decide cheapest viable route vs premium strategist. Choose Witsy vs Ollama vs paid API. Enforce cost and latency rules.

**Layer 3 — Researchers / Extractors.** Pull source data. Scrape or retrieve task inputs. Normalize into structured payloads for downstream layers.

**Layer 4 — Scorers / Classifiers.** First-pass issue scoring, clustering, categorization, priority assignment, evidence labeling.

**Layer 5 — Writers / Generators.** Create drafts. Produce reports. Generate structured outputs.

**Layer 6 — Critics / QA.** Challenge the draft. Verify fit against requirements. The critic is always a separate model from the writer — never self-review.

**Layer 7 — Publishers / Executors.** Save files. Update dashboards. Push outputs to storage. Hand off to implementation channels.

**Layer 8 — Monitors / Reporters.** Track status. Normalize metrics. Maintain workflow state.

## Free-first routing logic

The default execution rule: use the cheapest viable route. Escalate to paid or premium models only when the task genuinely requires it.

| Task type | Default route | Escalate when |
|---|---|---|
| Bulk extraction | Cheapest reliable worker | Extraction quality weak |
| Classification/scoring | Cheap structured worker | Ambiguity high |
| Strategic brief | Premium strategist | High-stakes scope |
| Draft writing | Strong generator | Quality weak |
| QA/critique | Separate critic model | Risk high |
| Local/private drafting | Ollama peer[^1] | Quality insufficient |

## The Witsy substrate

Witsy (local service, port 8090) functions as the primary delegation hub — routing tasks across an engine inventory spanning OpenRouter, Mistral, Google Gemini, Groq, Cerebras, OpenAI, Anthropic, DeepSeek, xAI, and Ollama.[^2]

Ollama operates as a peer local inference layer, not a subordinate Witsy dependency.[^1] Recommended use cases: local low-cost summarization, quick reasoning or coding helpers, preprocessing, private draft generation, and overflow work when central routes are constrained.

## Inbox/outbox protocol

Cross-agent handoff uses a structured message schema with defined status states:

```json
{
  "task_id": "uuid-or-timestamp",
  "agent_from": "source-agent",
  "agent_to": "target-agent",
  "instruction": "detailed task",
  "model": "preferred-model",
  "timeout_sec": 180,
  "priority": "normal"
}
```

Status states: received → running → complete → error → escalation needed.

## 7 workflow types

Each workflow is a defined chain from orchestrator to publisher — templates, not ad hoc decisions.

**Article generation:** SERP/top-10 extractor → factor matrix scorer → brief writer → article drafter → critic/SEO QA → publisher.

**GBP / local optimization:** Local research extractor → profile auditor → landing-page matcher → review/proof strategist → critic/QA → implementer/tracker.

**400-site audit:** Bulk extractor → first-pass classifier → issue clusterer → strategist summarizer → critic/QA → report generator. Core rule: do not use premium models on every site first.

**Marketing plan generation:** Baseline aggregator → package-fit scorer → roadmap drafter → critic/QA → dashboard initializer.

Additional workflow templates: image generation, video generation, dashboard/reporting.

## Cost discipline

- Default to free-first
- Reserve premium models for synthesis, executive QA, and genuinely hard reasoning
- Keep writer and critic separate — never self-review
- Do not burn premium tokens on bulk first-pass tasks

## Sources

[^1]: Ollama. *Local LLM Inference.* ollama.com. Open-source tool for running large language models locally via HTTP API. Used as a peer inference layer within the Zeus multi-agent stack.
[^2]: Witsy. *Multi-Provider AI Client.* witsyai.com. Desktop AI client supporting multiple LLM providers via unified API routing. Configured at port 8090 within the Zeus infrastructure.
