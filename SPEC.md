# makeoverlyonline — LOCKED SPEC
> READ THIS BEFORE TOUCHING ANYTHING. No exceptions.

---

## SITE IDENTITY
- Repo: `github.com/jmail482/makeoverlyonline`
- Live URL: `https://jmail482.github.io/makeoverlyonline/`
- Theme: hugo-profile (Go module — `github.com/gurusabarish/hugo-profile`)
- Hugo version: v0.147.6 at `/work/tools/hugo`
- Branch: `main` = source, `gh-pages` = published output

---

## LOCKED DECISIONS — DO NOT CHANGE WITHOUT EXPLICIT PERMISSION

### Navigation
- All nav links open **SEPARATE PAGES** (Option B — confirmed multiple times)
- Each page opens at the **top** (scrollY = 0)
- **NO** in-page anchor scroll, **NO** JS scroll hijacking
- **NO** `#` fragments in nav URLs
- Nav order: Home | About | Featured Work | Deep Case Study | Experience | Contact | Blog
- URLs: `/about/` `/featured-work/` `/deep-case-study/` `/experience/` `/contact/` `/case-studies/`

### Home Page
- **Hero section ONLY** — nothing else
- No "By The Numbers", no "Recent Case Studies", no About, no Featured Work
- One screen, no scrolling required
- `#recent-posts` hidden via `#recent-posts{display:none !important;}` in `layouts/partials/head/extensions.html`

### Hero Layout
- Photo: **LEFT**
- Content: **RIGHT**
- Title: **"Nishikawa."** (not "Hi, I'm Jonathan", not "I am Jonathan")
- Subtitle: "I make businesses visible where it counts."
- Stats bar: 14 | 138 | +104% | 4 (YEARS IN SEO | KPI REPORTS SHIPPED | KEYWORD LIFT (TWAG) | ACTIVE CLIENTS)
- Buttons: "View Case Studies" (primary/filled) + "Download Resume" (outlined)
- Social icons: LinkedIn, GitHub, Email

### About Page Layout
- Content: **LEFT**
- Photo: **RIGHT**

### Colors
- Background: pure white `#ffffff`
- All text: solid black `#000000`, `opacity: 1` (no gray, no opacity tricks)
- CSS overrides live in `layouts/partials/head/extensions.html` (loaded last, highest priority)
- **`assets/css/custom.css` is NOT reliably loaded — always use extensions.html**

---

## BUILD & DEPLOY — EXACT COMMANDS

### Build
```bash
export PATH="/work/tools/go/bin:$PATH" GOPATH=/work/tools/gopath GOCACHE=/work/tools/gocache
rm -rf public && /work/tools/hugo --gc --minify
```
- **NEVER pass `-b` flag** (breaks baseURL)
- Build time: ~18-25s

### Deploy (git worktree — rsync NOT installed, use cp -a)
```bash
git worktree remove /tmp/ghp --force 2>/dev/null
git worktree add /tmp/ghp gh-pages
cd /tmp/ghp
find . -maxdepth 1 -mindepth 1 ! -name '.git' -exec rm -rf {} +
cp -a /work/repos/makeoverlyonline/public/. .
touch .nojekyll
git add -A && git commit -m "Deploy: <description>"
git push origin gh-pages
cd /work/repos/makeoverlyonline && git worktree remove /tmp/ghp --force
```

### Preview (screenshot before deploy)
```bash
mkdir -p /tmp/preview/makeoverlyonline
cp -a public/. /tmp/preview/makeoverlyonline/
python3 -m http.server 8878 --directory /tmp/preview &
# Screenshot at: http://127.0.0.1:8878/makeoverlyonline/
# Must include /makeoverlyonline/ path for CSS to load correctly
export PLAYWRIGHT_BROWSERS_PATH=/work/tools/ms-playwright
/work/.kzvenv/bin/python playwright_screenshot.py
```
- **NEVER report "done" without an attached screenshot**
- GitHub Pages CDN cache = ~600s. Use `?v=YYYYMMDD[letter]` cache-busting suffix

---

## RULES FOR ALL FUTURE CHANGES

1. **Read this file first** — every session, every change
2. **Do only what was asked** — if something adjacent is broken, report it; do NOT fix it silently
3. **Screenshot before "done"** — no exceptions
4. **List what changed and what didn't** — after every change
5. **Never ask the same question twice** — if Jonathan answered it, it's in this file
6. **Never change nav behavior** — it's option B, separate pages, locked
7. **Never add sections to home page** — hero only, locked
8. **If a new request conflicts with this spec, flag it before acting**

---

## STILL NEEDED (user must provide)
- [ ] Real resume PDF → `static/files/jonathan-nishikawa-resume.pdf`
- [ ] Project screenshots (5) → `static/images/projects/`
- [ ] Verbatim testimonial quotes (3)
- [ ] Formspree form ID for contact form

---

## CURRENT STATE (as of 2026-06-01)
- main: `e054a3a`
- gh-pages: `f95a6bd` (deployed)
- Home: hero only ✅
- Photo left/content right ✅
- Black text ✅
- Hero title: `Nishikawa.` — with dot (matches LOCKED) ✅
- Social icons in hero: LinkedIn, GitHub, Email (matches LOCKED) ✅
- All nav = separate pages ✅
- Section pages live: /about/ /featured-work/ /deep-case-study/ /experience/ /contact/ ✅
- Section pages generated via `content/{page}.md` with `type: sectionpage` ✅
- Recent posts hidden ✅
- Nav logo (broken img) removed ✅
- Search bar removed ✅
- Dark mode toggle removed ✅
- Footer branding ("Made with Hugo Profile") removed ✅
- Footer social icons removed ✅
- Footer logo image removed ✅
- Footer = `© 2026 Jonathan Nishikawa. All Rights Reserved.` only ✅
- Hero empty space fixed (min-height:auto) ✅
- FontAwesome: local JS (6.4.2) ✅
- style.css 404 fixed ✅

## STILL NEEDED (awaiting Jonathan's assets)
- Real resume PDF → `static/files/jonathan-nishikawa-resume.pdf`
- Project screenshots (5) → `static/images/projects/`
- Verbatim client testimonials (3)
- Formspree form ID for contact form

## CHANGELOG
### 1392a3c (2026-06-01)
- `hugo.yaml`: `showBrandLogo: false`, `disableSearch: true`, `socialNetworks: {}`
- `extensions.html`: `#theme-toggle{display:none}`, hero `min-height:auto`, button `margin-top:0`, footer styles
- `layouts/partials/sections/footer/copyright.html`: clean copyright override
- `layouts/partials/sections/footer/socialNetwork.html`: empty (no icons)
- `layouts/index.html`: FA JS replaced with FA 6.4.2 CSS CDN
- `static/style.css`: created (fixes 404)
