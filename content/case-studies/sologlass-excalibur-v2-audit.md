---
title: "Sologlass.ca: A 4.9-star ICBC-certified auto glass shop invisible to every search — and 24 steps to fix it"
date: 2025-08-13T10:00:00-05:00
draft: false
tags: ["case study", "technical SEO", "local SEO", "ICBC", "Excalibur", "auto glass"]
categories: ["case studies"]
description: "Solo Glass had a 4.9-star Google rating, 149+ reviews, two locations, and ICBC certification. From their South Surrey address, they ranked for zero keywords — organic, Map Pack, and AI Overviews all blank. The Excalibur V2 engine diagnosed why."
summary: "A two-location BC auto glass shop with exemplary real-world credentials produced an overall digital health score of 38/100. The audit found the /about/ page ranking for 11 service keywords, footer links pointing to a development server on every page, HTTP and HTTPS indexed as separate pages, and zero digital presence from the Surrey location. A 24-step roadmap sequenced the fix."
stat: "$450K–$1.5M"
statLabel: "Revenue Leakage"
statSubtitle: "Sologlass · 4.9★ · ICBC Certified"
cover:
  image: "/makeoverlyonline/images/case-studies/sologlass-excalibur-v2-audit.jpg"
  alt: ""
  caption: ""
ShowToc: true
TocOpen: false
---

## Forensic Audit Case Study: The Invisible 5-Star Authority

**Strategic Focus:** Technical Infrastructure & Revenue Recovery

## The business

Solo Glass is an ICBC-certified, ITA government-certified auto glass shop operating two locations in BC: Langley (#104 – 22575 Fraser Hwy) and South Surrey (1706 152 Street) [site crawl, Apr 2026]. Their Google rating: 4.9 stars across 149+ reviews [Google Business Profile, Apr 2026]. They offer a lifetime warranty on workmanship, mobile service, and proprietary GlassHealer resin. Family-owned against national franchise competitors NOVUS (Mondofix) and Speedy Glass (Belron).

*Excalibur V2 audit generated April 25, 2026. Data: SEO PowerSuite Rank Tracker v8.50.18 geo-located from both business addresses [SEO PowerSuite][^1]. Overall Digital Health Score: 38/100.*

## What the audit found

Five total pages [site crawl, Apr 2026]. Zero schema markup anywhere [site crawl, Apr 2026]. Homepage loading in approximately 5 seconds — estimated 35% conversion loss before a visitor sees content, based on a documented 7% conversion reduction per second of load delay [SteerPoint, 2025][^2].

From the Langley address: 11 keywords tracked, zero organic traffic [SEO PowerSuite Rank Tracker, Apr 2026][^1]. Best position: #18 for "windshield replacement langley" (150 searches/month, CPC $6.84 [SEO PowerSuite Rank Tracker][^1]) — on the /about/ page, not the /services/ page. Three keywords appearing as thumbnail results only (near-zero click value). Click-through rates at position 18 approach 0% [Advanced Web Ranking CTR study][^3].

From the South Surrey address: complete blackout. Zero organic rankings. Zero Map Pack rankings. Zero AI Overview appearances [SEO PowerSuite Rank Tracker, Apr 2026][^1]. "Auto glass repair surrey" — not in the top 30.

## Four critical failures

**1. HTTP/HTTPS dual indexing.** Rank Tracker confirmed both `http://sologlass.ca/` and `https://sologlass.ca/` were indexed as separate pages, splitting all ranking signals between them [SEO PowerSuite Rank Tracker][^1]. Per Google's canonical documentation, duplicate URL indexing dilutes ranking signals [^4].

**2. Dev server links in footer.** Every page carried footer Quick Links — all pointing to `dev3.boost-digital.ca` instead of `sologlass.ca` [site crawl, Apr 2026]. The /services/ page additionally carried an image hosted on `ejw.f33.mytemp.website` [site crawl, Apr 2026].

**3. Wrong page ranking for all service keywords.** The /about/ page ranked for 11 keywords. The /services/ page ranked for one [SEO PowerSuite Rank Tracker][^1]. Per Moz local ranking factors research, a location page with consistent NAP and schema is foundational to local visibility [^5].

**4. Every title tag and image alt text said "Langley."** Five pages, all titled for Langley only [site crawl, Apr 2026]. Per Google's Images documentation, alt text carries geographic relevance signals [^6].

## The competitive context

NOVUS Glass South Surrey holds ICBC Tier 1 Top Performer status — listed first on ICBC's official repair locator [ICBC Glass Repair Program Guide, Oct 2024][^7]. Tier 1 requires a 35%+ windshield repair ratio and delivers a 2% NAGS part rebate, $75/repair claim, and faster payment cycles [ICBC Glass Repair Program Guide][^7]. Braymar Glass has operated in South Surrey/White Rock for 25+ years [Peace Arch News][^8].

All 11 tracked keywords showed green difficulty ratings (10–23 range) [SEO PowerSuite Rank Tracker][^1] — low difficulty that proper page structure would rank for.

## The 24-step roadmap

**Phase 1 — 3 months:** Force HTTPS canonical sitewide. Fix dev server links. Diagnose and resolve 5-second homepage load. Build /langley/ and /south-surrey/ dedicated location pages with LocalBusiness + AutoRepair JSON-LD schema. Build /white-rock/ service area page. Fix all page titles and image alt text sitewide. Add FAQPage schema to existing 13 FAQs [site crawl, Apr 2026]. Configure GBP profiles to location pages. Launch Surrey review generation program (target: 15+ Surrey reviews within 90 days).

**Phase 2 — 6 months:** Dedicated service pages. ICBC claims landing page. ADAS calibration investigation. Service area pages. Blog launch.

**Phase 3 — 12 months:** Content hub (15–20 interlinked pages around ICBC + BC auto glass). YouTube video content. GEO optimization. Sustained review velocity — target: 350+ combined reviews across both GBPs.

## What this demonstrates

Auto glass in BC is an insurance-paid category — ICBC covers windshield repair and replacement directly [ICBC Glass Repair Program Guide][^7]. The conversion bottleneck is not price or persuasion. It is visibility. The 24 items were a dependency chain, not a list.

## Quantified revenue leakage

The 38/100 Digital Health Score is not a number — it is a dollar figure. Mapping current visibility against market demand in the Surrey / White Rock / Cloverdale corridor (combined population ~500,000) yields an estimated **$450K–$1.5M in annual revenue leakage**: traffic and ICBC-paid claims that legacy local competitors and franchise chains (NOVUS, Speedy Glass) are capturing because Solo Glass has zero presence in queries originating south of the Fraser. Once the 3-month structural rebuild executes, even partial market re-entry compounds against an audience that is mandated by ICBC to use a certified shop.

## What I'd do differently

In hindsight, the audit should have led with the dev-server footer link, not with HTTP/HTTPS. Both are P0 issues, but the dev-server footer was actively bleeding crawl equity to a domain Solo Glass doesn't control — a structural problem that would have undermined every other fix until resolved. Sequencing the diagnosis from "loudest signal" (the keyword/page mismatch) to "most-load-bearing failure" (the footer) inverted the dependency chain a second time. The 24-step roadmap got it right; the audit narrative didn't.

I'd also defer the speed/Core Web Vitals work behind the architectural fixes. A 5-second load time matters, but only after the right pages are ranking for the right queries. Speed work on a /about/ page that shouldn't be ranking for service queries is wasted effort.

## Sources

[^1]: SEO PowerSuite. *Rank Tracker v8.50.18.* link-assistant.com. Geo-located rank tracking configured from both Solo Glass business addresses (Langley and South Surrey) for the April 2026 audit.
[^2]: SteerPoint. *Why Website Speed Is More Important Than Ever in 2025.* 2025. Documents 7% conversion reduction per additional second of page load time.
[^3]: Advanced Web Ranking. *Organic CTR Study*, 2024–2025. Position 18 produces near-zero click-through rates under standard organic CTR distribution curves.
[^4]: Google Search Central. *Consolidate Duplicate URLs.* developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls.
[^5]: Moz. *Local Search Ranking Factors*, 2025. Location page with consistent NAP and LocalBusiness schema documented as a foundational local signal.
[^6]: Google Search Central. *Google Images Best Practices.* developers.google.com/search/docs/appearance/google-images.
[^7]: ICBC. *Glass Repair Program Guide (CSP51).* Effective October 1, 2024. partners.icbc.com.
[^8]: Peace Arch News. *South Surrey Auto Glass Repair Shop Responds to ICBC Changes*, 2023.
