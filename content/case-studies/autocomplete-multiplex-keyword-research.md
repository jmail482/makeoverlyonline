---
title: "autocomplete_multiplex.py: Routing keyword research across three API backends with automatic failover and credit tracking"
date: 2025-11-08T10:30:00-05:00
draft: false
tags: ["case study", "Python", "keyword research", "automation", "API", "CDCP"]
categories: ["case studies"]
description: "A Python keyword research multiplexer that routes different AI agents to different API backends — Serper, ScrapFly, and direct Google Autocomplete — with automatic failover, per-backend credit tracking, and usage logging. Built to support large-scale CDCP dental keyword research."
summary: "autocomplete_multiplex.py was built to solve a practical problem: running keyword autocomplete queries at scale across a multi-agent AI infrastructure where different agents have different API access, credit pools are finite and backend-specific, and no single backend is reliable enough to run the full workload alone. The solution is a routing layer that matches agent to backend by policy, tracks spend per backend, logs usage, and fails over automatically."
stat: "3"
statLabel: "API Backends · Failover"
statSubtitle: "Routing Keyword Research · Credit Tracking"
cover:
  image: "/makeoverlyonline/images/case-studies/autocomplete-multiplex-keyword-research.jpg"
  alt: ""
  caption: ""
ShowToc: true
TocOpen: false
---

## The problem

Keyword autocomplete research at scale requires running hundreds of seed queries against Google's suggestion endpoint. Running all queries through a single API backend creates three failure modes: credit exhaustion, rate limiting, and single-point-of-failure for a critical research step.

The project context: a large-scale CDCP dental keyword research project requiring autocomplete data across multiple query clusters simultaneously, with different AI agents executing different portions of the workload.

## The routing architecture

The multiplexer routes each incoming query to a backend based on which agent is making the request:

| Agent | Primary Backend | Fallback |
|---|---|---|
| Claude / Opus | Serper[^1] | ScrapFly[^2] |
| Haiku | ScrapFly[^2] | Direct Google[^3] |
| G1 (Zeus File Bridge) | Direct Google[^3] | ScrapFly[^2] |
| G3 / Qwen | ScrapFly[^2] | Direct Google[^3] |

The routing logic is policy-driven, not dynamic. Each agent has a defined primary and a defined fallback. The multiplexer checks credit availability on the primary backend before routing; if the primary is exhausted or unavailable, the request goes to the fallback automatically.

## Credit tracking

Each backend maintains a separate credit pool. The multiplexer tracks requests sent per backend per session, estimated credits consumed per request (by backend pricing model), a running total against configured per-backend limits, and an alert threshold before exhaustion. Usage is logged per-request with timestamp, agent, backend used, query, and credit cost.

## Backend characteristics

**Serper**[^1] — paid API, highest reliability, cleanest JSON response, rate limits apply per API key. Primary for Claude/Opus because Claude-originated research tasks are typically the highest-priority and most complex.

**ScrapFly**[^2] — paid scraping proxy, higher latency than Serper, better suited for volume tasks where per-request cost matters more than speed.

**Direct Google Autocomplete**[^3] — zero cost, no API key required (endpoint confirmed working), latency variable, subject to rate limiting from Google's side if request volume is high. Primary for G1 (Zeus) which runs against the infrastructure at high frequency.

## Output structure

Outputs go to `Auto Suggest Scraper V2/engine/` and `outputs/`. Each file contains: seed query, backend used, timestamp, raw autocomplete suggestions returned, and normalized suggestion list — compatible with downstream keyword clustering and intent classification pipelines.

## Sources

[^1]: Serper. *Google Search API.* serper.dev. JSON API for Google Search and Autocomplete results. Used as primary backend for Claude/Opus agent queries.
[^2]: ScrapFly. *Web Scraping API.* scrapfly.io. Rotating proxy and scraping infrastructure used as primary backend for Haiku and G3/Qwen agent queries.
[^3]: Google. *Google Autocomplete (Search Suggestions).* Undocumented public endpoint (google.com/complete/search). Zero cost, no authentication required. Used as primary backend for G1 (Zeus File Bridge) agent queries.
