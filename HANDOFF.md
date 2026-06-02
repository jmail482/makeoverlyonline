# makeoverlyonline — Editing Handoff (for any LLM/dev)

Complete instructions to safely edit and ship the live site.
**Live URL:** https://jmail482.github.io/makeoverlyonline/

---

## 1. Repo & access
- **GitHub:** `github.com/jmail482/makeoverlyonline` (account `jmail482`, NOT `jnish1964-a11y`).
- Auth: a Personal Access Token with `repo` scope. The token does **NOT** have `workflow` scope, so the deploy is **manual** (see §4). Token is embedded in the local clone's git remote.
- Branches:
  - `main` — **source of truth** (Hugo source: layouts, content, config). Edit here.
  - `gh-pages` — **published output** (pre-built static HTML). GitHub Pages serves THIS branch. Never hand-edit; it's overwritten on every deploy.

## 2. Stack
- **Hugo** (static site generator), theme **`github.com/gurusabarish/hugo-profile`** pulled as a Hugo Module (`go.mod` / `module.imports` in `hugo.yaml`).
- Bootstrap 5 + FontAwesome 6 (vendored in repo: `bootstrap-5/`, `fontawesome-6/`).
- No JS framework. Single-page hero + standalone section pages.

## 3. File map — WHERE TO EDIT WHAT
| Want to change… | Edit this |
|---|---|
| Hero text, name, stats, image, buttons, social links | `hugo.yaml` → `params.hero` |
| Nav menu items / order | `layouts/partials/sections/header.html` (hardcoded `<li>` links) + `params.navbar` |
| Logo / brand lockup | `layouts/partials/sections/header.html` (`.navbar-brand` block) + `static/images/makeoverly-mark.svg` |
| All custom styling / colors / overrides | `layouts/partials/head/extensions.html` (two `<style>` blocks) |
| Hero layout/HTML (social row, button column) | `layouts/partials/sections/hero/index.html` |
| About / Experience / Contact / Featured Work / Deep Case Study copy | `content/*.md` + matching `params` sections in `hugo.yaml` |
| Section component HTML | `layouts/partials/sections/about.html`, `deep-case-study.html`, `testimonials.html` |
| Case study / blog pages | `content/case-studies/` style pages via `layouts/sectionpage/single.html` |

### Theme override mechanism (IMPORTANT)
Files under `layouts/` in THIS repo **override** the same-path files in the theme module. E.g. `layouts/partials/sections/header.html` shadows the theme's `partials/sections/header.html`. To customize a theme partial, copy it from the module into the matching local `layouts/` path and edit the copy. Current overrides: `header.html`, `hero/index.html`, `head/extensions.html`, `about.html`, `deep-case-study.html`, `testimonials.html`, `index.html`, `404.html`, `sectionpage/single.html`.

## 4. Build & deploy (manual — do exactly this)
From repo root on `main`:

```bash
# 1. Build (NEVER pass -b/--baseURL; baseURL is already in hugo.yaml)
hugo --gc --minify          # outputs to ./public/

# 2. Commit source changes to main
git add -A && git commit -m "..." && git push origin main

# 3. Deploy built output to gh-pages via a worktree
git worktree add /tmp/ghp gh-pages
cd /tmp/ghp
find . -maxdepth 1 -not -name '.git' -not -name '.' -exec rm -rf {} +
cp -r /path/to/repo/public/* .
touch .nojekyll                      # REQUIRED — stops Jekyll from eating _-prefixed assets
git add -A && git commit -m "Deploy: ..." && git push origin gh-pages
cd - && git worktree remove /tmp/ghp --force
```
GitHub Pages rebuilds in ~60–90s. Static assets (e.g. the SVG mark) often go live before the HTML finishes re-propagating — re-check after a minute.

> Why manual: the token lacks `workflow` scope, so a GitHub Actions auto-deploy can't be pushed. The worktree method publishes pre-built HTML directly to `gh-pages`, which Pages serves as-is.

## 5. Local preview (subpath-correct)
The site lives under the `/makeoverlyonline/` subpath, so serving `public/` at root breaks asset/links. Mirror the subpath:
```bash
mkdir -p serveroot && ln -sfn /path/to/repo/public serveroot/makeoverlyonline
cd serveroot && python3 -m http.server 8911
# open http://127.0.0.1:8911/makeoverlyonline/
```

## 6. Key config highlights (`hugo.yaml`)
- `baseURL: https://jmail482.github.io/makeoverlyonline/`
- `params.color.*` all set to pure black/white (B/W editorial direction).
- `params.animate: false` (scroll/jump animations disabled).
- `params.navbar.align: me-auto` → nav sits LEFT, beside the logo. `brandName: ""` + `showBrandLogo: false` because the brand is rendered manually in `header.html`.
- `params.hero`: title `Nishikawa.`, subtitle, content, `image: /makeoverlyonline/images/profile.jpg`, 4 `stats`, `button` (View Case Studies → `/makeoverlyonline/case-studies`), `resumeButton` (→ `/makeoverlyonline/files/jonathan-nishikawa-resume.pdf` — **PDF not uploaded yet**), and `socialLinks.fontAwesomeIcons` (LinkedIn / GitHub / Email, each with `icon`, `url`, `label`, `color`).

## 7. Custom CSS architecture (`layouts/partials/head/extensions.html`)
Two `<style>` blocks. Design intent = strict black-on-white, Inter font, no theme accent colors.
- **Global override:** `*{ color:#000 !important }` forces black text everywhere (kills theme's gray/opacity). ⚠️ **Gotcha:** this also blacks out icon glyphs. Any white/colored glyph must beat it with higher specificity, e.g. `#hero .hero-social-row .social-ic i{ color:#fff !important }`.
- **Hero left column** (most recently customized):
  - `.hero-social-row` — social icons in a **horizontal row** under the photo: small (34px), **monochrome**, transparent circle with `1.5px #d4d4d4` border, dark glyph, fills black on hover. (No brand colors, no labels/pills.)
  - `.hero-buttons-left` — the two CTA buttons stacked in a **column** below the social row; both forced to the **same** solid-black style (identical look), `width:100%`, `max-width:240px`.
- **Brand lockup:** `.brand-mark` (SVG, ~30px), `.brand-word` (Inter, bold), `.brand-accent` (the "ly", emerald `#19B36B`).

## 8. Branding assets
- `static/images/makeoverly-mark.svg` — the logo icon: black rounded tile + white upward growth-arrow + emerald `#19B36B` accent arrowhead. SVG = scales crisp at any size. The "makeoverly" wordmark next to it is **HTML text** (in `header.html`), not baked into the SVG, so it uses the page's Inter font.
- `static/images/profile.jpg` — hero portrait (B/W treatment applied via CSS).

## 9. Content
`content/about.md`, `contact.md`, `deep-case-study.md`, `experience.md`, `featured-work.md`. Deep Case Study holds real TWAG client data. Most structured data (experience roles, testimonials, project cards) lives in `hugo.yaml` `params`, not the markdown.

## 10. Lessons / preferences (owner = Jonathan)
- **Aesthetic:** minimal, professional, monochrome black/white. **No** colored pills, badges, labels, or decorative accents unless explicitly asked. Keep it clean.
- **Always browser-verify the LIVE github.io URL** after deploying before claiming it's done. Don't trust the build alone; don't blame browser cache.
- Keep `main` (source) and `gh-pages` (built) in sync — if you push source but forget the gh-pages deploy, the live site won't change.
- Don't add `-b`/`--baseURL` to the hugo build; it double-prefixes the subpath and breaks links.

---
_Last updated after: smaller monochrome social icons + identical CTA buttons (commit on `main`)._
