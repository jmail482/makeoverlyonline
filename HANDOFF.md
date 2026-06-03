# makeoverlyonline — POINTER FILE

> ⚠️ **THIS FILE IS A STUB. DO NOT TRUST ITS CONTENTS FOR CURRENT SITE STATE.**
> Previous versions of this file kept full project state inline and went stale within hours.
> The earlier 2026-06-01 version described Nishikawa-with-period, 4 stats, enabled hero buttons, and Linux build paths — none of which are current.
>
> **Read `hugo.yaml` for current config. Read the active session's `HANDOFF_PACKAGE.md` for active state.**

---

## Where canonical truth actually lives

| What you need | Where to look |
|---|---|
| Current site config (params, content, deploy URL) | `hugo.yaml` |
| Active session state (deploys, open loops, recent edits) | `~/.runner/workspaces/*/sessions/*/HANDOFF_PACKAGE.md` (sort by mtime, take newest) |
| Custom CSS / layout overrides | `layouts/partials/head/extensions.html`, `layouts/partials/sections/*.html` |
| Case study content (23 files) | `content/case-studies/*.md` |
| Deploy procedure | Skills DB id 1145 (`hugo-profile-deploy-makeoverlyonline`) or the session's `skill_deploy_makeoverlyonline.md` |
| Theme params reference | `~/.runner/memory/reference_hugo_profile_theme.md` |
| Known gotchas (CRLF kills nested params, AI-image blanks, alignment magic numbers) | `~/.runner/memory/feedback_*.md` (search keyword `hugo` or `image`) |
| Live URL (always check first) | https://jmail482.github.io/makeoverlyonline/ |
| Source branch / deploy branch | `main` = source, `gh-pages` = published HTML |

## Rule for any future LLM picking up work here

1. **DO NOT** treat this file as current state.
2. Read `hugo.yaml` to see what's actually configured.
3. Find the most recent `HANDOFF_PACKAGE.md` under `~/.runner/workspaces/*/sessions/*/`.
4. Browse the live URL before making assumptions.
5. **DO NOT** add project state to this file. Anything you put here is stale within the day.
6. If the recruiter spec or design decisions need a long-form home, put them in `~/.runner/memory/project_makeoverlyonline_portfolio.md` (file memory survives sessions; this file does not).

## How to verify this file is still a pointer and not a content file

If anything in this file describes specific stats, button labels, hero text, file paths beyond canonical anchors, or commit SHAs — it's drifted. Restore it to a pointer.

Last stubbed: 2026-06-02
