---
title: "makeovelry.com: Building and deploying a Hugo portfolio site via GitHub Actions in a single session"
date: 2025-12-09T12:30:00-05:00
draft: false
tags: ["case study", "Hugo", "GitHub Pages", "portfolio", "web development"]
categories: ["case studies"]
description: "A static portfolio site built on Hugo with the PaperMod theme, deployed to GitHub Pages via a GitHub Actions CI/CD pipeline. From zero to 13 live case study posts in one working session — including diagnosis and fix of a structural rendering issue that was hiding the entire posts section."
summary: "makeovelry.com is a STAR-format portfolio presenting SEO and digital marketing case studies, built on Hugo Extended with PaperMod, hosted on GitHub Pages at jmail482.github.io/makeovelry. The project documented every technical obstacle encountered: an empty _index.md hiding the posts section, a directory restructure that put case study posts in the wrong location, a Hugo server not installed locally, and the resolution via GitHub Actions automation."
stat: "1 session"
statLabel: "Hugo Portfolio Build"
statSubtitle: "GitHub Actions · Live Deploy"
cover:
  image: "/makeoverlyonline/images/case-studies/makeovelry-hugo-portfolio-build.jpg"
  alt: ""
  caption: ""
ShowToc: true
TocOpen: false
---

## The project

makeovelry.com (hosted at jmail482.github.io/makeovelry) is a professional portfolio built to present SEO and digital marketing case studies in a STAR format — Situation, Task, Action, Result — with each post card showing a date, reading time, 2–3 sentence description, and tag pills matching the visual style of the Hugo PaperMod theme.

## Stack

- **Framework:** Hugo Extended (latest)[^1]
- **Theme:** PaperMod[^2]
- **Hosting:** GitHub Pages (jmail482/makeovelry repository)[^3]
- **CI/CD:** GitHub Actions (hugo.yml workflow — triggers on every push to main)[^4]
- **Content management:** Markdown files in /content/blog/

## The structural issue that hid the posts section

The initial site build had posts section invisible despite files existing on disk. Root cause: `/content/posts/_index.md` was empty except for the title. Hugo treats a section without `draft: false` in the front matter as a draft and hides it from the rendered site.[^1]

Fix: add `draft: false` to `_index.md`. Posts list rendered immediately.

## The directory restructure catch

Nine case study posts were written to `/content/posts/` and committed to GitHub. They did not appear on the site. Investigation revealed: the remote repository had been restructured — posts moved from `/content/posts/` to `/content/blog/` — in a commit that was not in the local repository.

The `git push` had failed silently (Status Code: 1) because the remote contained commits the local branch did not have. The correct sequence:

1. `git pull origin main` — merged remote restructure into local (confirmed directory rename via merge output)
2. Moved all 9 files from `/content/posts/` to `/content/blog/`
3. `git add`, `git commit`, `git push` — confirmed clean push (Status Code: 0)

## The GitHub Actions deployment

Hugo was not installed locally. A GitHub Actions workflow was written to build and deploy automatically on every push to main:[^4]

```yaml
name: Build and Deploy Hugo Site
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true
      - run: hugo --minify
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

## Current state

21 posts live as of May 2026 across three groups: historical client case studies (Appendix B), recent audit and research case studies, and systems and infrastructure case studies.

## Sources

[^1]: Hugo. *Hugo Extended — Static Site Generator.* gohugo.io. Front matter draft flag behaviour and section list rendering documented in Hugo content management documentation.
[^2]: Adityatelange. *PaperMod — Hugo Theme.* github.com/adityatelange/hugo-PaperMod. Open-source Hugo theme used for portfolio styling.
[^3]: GitHub Pages. *GitHub Pages Documentation.* docs.github.com/en/pages. Static site hosting from GitHub repositories. Configured for jmail482/makeovelry.
[^4]: peaceiris. *actions-hugo and actions-gh-pages.* github.com/peaceiris. GitHub Actions used for automated Hugo build and GitHub Pages deployment on push to main.
