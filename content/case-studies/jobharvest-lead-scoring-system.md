---
title: "JobHarvest: A scoring and filtering system for SEO job leads — built because most job boards waste your time"
date: 2024-11-26T13:30:00-05:00
draft: false
tags: ["case study", "automation", "job search", "lead scoring", "Python"]
categories: ["case studies"]
description: "JobHarvest is a job lead filtering and scoring system built to eliminate the 75%-match-or-reject threshold problem in SEO job searching. It filters for role fit, flags EU/non-remote locations, removes junior roles, and scores remaining leads against a documented skills profile — all without generating filler leads."
summary: "Senior SEO job searching without a filter system produces noise: junior roles, EU-only listings, mismatched titles, and remote-listed roles that turn out to be location-specific. JobHarvest applies a 75% match threshold minimum, removes filler, and scores leads against a documented profile. Methodology documented in HOW_SCORING_WORKS.md (688 lines)."
stat: "Score"
statLabel: "SEO Job Leads"
statSubtitle: "Built Because Job Boards Waste Time"
cover:
  image: "/makeoverlyonline/images/case-studies/jobharvest-lead-scoring-system.jpg"
  alt: ""
  caption: ""
ShowToc: true
TocOpen: false
---

## The problem with raw job boards

Senior SEO job searching against raw job board output produces predictable noise: junior roles labelled as "specialist," EU-only listings appearing in Canadian remote searches, titles like "Digital Marketing Coordinator" mixed with "SEO Lead," and roles requiring skills stacks that don't match a Local SEO / Technical SEO specialist profile.

Running this noise through manual review costs time and produces frustration, not leads. The solution is a filter-first system.

## The scoring methodology

JobHarvest applies a documented scoring methodology (HOW_SCORING_WORKS.md, 688 lines[^1]) before any lead reaches review.

**Hard exclusions applied before scoring:**
- EU and non-Canadian international locations (even when listed as remote)
- Junior-level roles (Coordinator, Assistant, Entry Level by title or JD signal)
- Roles requiring primary expertise outside the documented skills profile

**Match threshold:** 75% minimum. Below 75%, the lead is excluded without review.

**Scoring inputs:**
- Role title alignment to target titles: SEO Specialist / SEO Lead / SEO Manager / Digital Marketing Specialist
- Location: remote Canada or Winnipeg on-site preferred; other on-site excluded
- Skills overlap against documented profile (Local SEO, Technical SEO, GBP, WordPress, Google Ads, Meta Ads[^2])
- Seniority signal from JD language and required years of experience

**Resume sources used for matching:** Resume.txt, resume data sheet.txt, old stuff i could beef my resume up with.txt. Not the standard one-page resume file — the one-page format obscures experience depth that the scoring system needs to assess.

## Top leads identified

The system produced actionable leads at or above the 75% threshold:

- **Webrunner Media — Senior SEO Lead** — strong title match, Canadian remote, agency context aligned to service profile[^3]
- **CareForMix — Digital Marketing Specialist** — healthcare sector, remote Canada, skills overlap confirmed[^3]
- **GCOM Support — SEO Specialist** — technical SEO emphasis, confirmed Canadian, role scope aligned[^3]

## What the system does not do

JobHarvest does not auto-apply. It does not send emails. It does not generate cover letters. It produces a filtered, scored lead list and stops there. Human judgment handles everything past the scoring output.

No conversion-to-interview rate is documented. No offer data exists. The system's value is in the front-of-funnel: eliminating noise and surfacing leads worth manual time.

## Sources

[^1]: HOW_SCORING_WORKS.md. 688 lines. Documents the full scoring methodology, threshold rules, and exclusion logic.
[^2]: Resume data sheet.txt and Resume.txt. Skills profile source files used for match scoring.
[^3]: Indeed.ca; LinkedIn.ca. Job postings verified at time of lead identification, 2026. Lead details on file in job-scraper project outputs.
