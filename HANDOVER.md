# Handover — dominichu93.github.io redesign

_Last updated: 2026-06-26. Read `CLAUDE.md` first for the system prompt / design rules._

## Context
Dom's personal site was a dark, hand-built vanilla HTML/CSS portfolio that had accumulated bugs,
fragmented styling (per-page inline `<style>` blocks, two button blues), ~31 MB of unoptimised
images, and missing SEO. We did a deep technical review, then redesigned it.

## What was done (this iteration)
- **Full redesign to a Bouke-inspired, monochrome, Space Grotesk system.** Dark by default with a
  **light/dark toggle** (cream + ink in light), one foreground colour, uppercase bold name, no italics,
  no accent colours.
- **Consolidated all styling into a single `style.css`** built on CSS variables (theme tokens). Removed
  every per-page inline `<style>` block.
- **Rebuilt every page on the shared stylesheet:** `index.html` (home) + posts
  `country-manager-uk.html`, `monumental-8-months.html`, `new-roles.html`,
  `full-stack-swe-kreekrijk.html`, plus `projects.html` (now a clean Writing index).
- **Homepage masthead:** name top-left, "I build teams." as a subtitle, intro paragraph, portrait on the
  right (sized 338px — 25% larger than the prior 270px), spaced like the original.
- **Content cleanup:** cut **all emojis** from the 8-months post; replaced **all em dashes with hyphens**
  site-wide; removed the old blue link colour everywhere.
- **Bug fixes from the audit:** fixed the broken drone image (`new-roles.html` now points at
  `images/new-roles-dji.jpg`), fixed unclosed/stray tags, added `rel="noopener"` to all external links,
  added per-page `<title>` + meta description + Open Graph/Twitter cards + favicon, normalised `lang`.
- **A11y:** visible focus rings, `prefers-reduced-motion` handling, AAA-ish contrast in both themes.

## Open task list (prioritised)
1. **Image compression (biggest perf win, not yet done).** `RobotPhoto.jpg` ≈ 18 MB and
   `images/new-roles-dji.jpg` ≈ 19 MB are still full-resolution. Resize to display size, export WebP
   with JPEG fallback, add `width`/`height` (+ `srcset` where useful). Target each ≤ ~300 KB.
2. **Dead-file cleanup (needs Dom's OK — these predate us / are scratch).** Candidates to delete:
   `Atrium_ The Operating System for Software-Defined Construction.html` (stray Webflow dump),
   `reddit-preview.jpg` (actually an HTML file mislabeled `.jpg`, ~4 MB), `IMG_6384 (1).jpeg` (unused,
   ~5 MB). The scratch `demo-*.html` and `style.new.css` files were removed during deploy.
3. **LinkedIn / Reddit embeds render as bright white cards in dark mode** (`country-manager-uk.html`,
   `new-roles.html`) — third-party iframes we can't restyle. Optional: replace with a dark pull-quote of
   the text + a "View on LinkedIn/Reddit" link so every page stays fully dark. Vimeo embeds are already
   dark and fine.
4. **New subpages.** Dom will provide media + text for new posts. Build each with the post template
   (see `CLAUDE.md` → "Adding a new post page") and add it to the Writing list in `index.html` and
   `projects.html`.
5. **Nice-to-haves:** `robots.txt` + `sitemap.xml`; a small optimised dedicated OG share image
   (currently OG points at full-size photos).

## Deploy
GitHub Pages serves `main` branch root. `git add -A && git commit && git push origin main` → live in
~1 min at https://dominichu93.github.io/. The local folder is wired as a git repo tracking `origin/main`.

## Key files
- `style.css` — the whole design system (tokens, themes, masthead, post layout, embeds, toggle).
- `index.html` — homepage (masthead + About + Writing list).
- `*.html` posts — each self-contained, linking `style.css`.
- `images/` — site imagery. Root-level `your-hero-image.jpg` is the homepage portrait (engraving).
