# nowlin.io redesign — DESIGN.md

## Design read

Reading this as: a personal site for James Nowlin (Garland County Library
Outreach Coordinator / bookmobile operator, UNT MLS student, homelab nerd),
with a plain-spoken, funny, no-bullshit language, leaning toward
editorial-brutalist dark.

Dials: **variance 7 / motion 2 / density 4**. Asymmetric left-aligned hero,
mixed layout families per section, hover-only motion (transform/opacity),
comfortable editorial spacing. Audited against the design-taste skill:
no em-dashes, no numbered-section eyebrows, one accent color, hero fits
the first viewport, reduced-motion respected.

## What changed

**New custom theme `themes/nowlin/`** (PaperMod retired, left in `themes/`
untouched for rollback). Everything is hand-rolled: no frameworks, no
build-time JS, zero client JS at all (mobile nav is a checkbox hack).

- **Palette:** Nord-inspired dark. Off-black blue-tinted background
  (`#12151c`), raised surfaces, one accent (burnt orange `#d08770`),
  frost blue reserved for links. No gradients-as-decoration.
- **Type:** self-hosted woff2 in `static/fonts/` — Archivo 700/800/900
  (display, tight tracking, uppercase heroes), Inter 400–700 (body),
  IBM Plex Mono 400–600 (kickers, dates, meta labels). No Google Fonts CDN.
- **Home:** oversized "JAMES / NOWLIN" hero (second line outlined),
  one-line kicker, ~20-word sub, three CTAs. Four nav cards
  (About / Blog / eFolio / Hobbies). A stats strip with James-isms
  (bookmobile, MLS, homelab, "0 flatpaks installed"). Latest-writing feed.
- **Blog:** editorial date-ordered rows, not cards. Reading time + word
  count meta, older/newer post nav.
- **eFolio (`/unt-mls/`):** custom landing grouping the real structure —
  Education (1.0–1.3), Professional Development (2.0–2.2), Reflections
  (nested posts section). All seven pages and both reflection posts intact,
  every alias preserved.
- **Header/footer:** sticky blurred nav with active-section marker,
  footer with real social SVGs, colophon ("No trackers, no cookies,
  no nonsense.").
- **404:** on-brand ("wandered off like a bookmobile with a bad GPS").
- **Code blocks:** Chroma `nord` style, generated via
  `hugo gen chromastyles`.

## Technical notes

- Builds clean with `hugo --minify` (0.152.2 extended): 30 pages,
  20 aliases (all front-matter aliases resolve), RSS + sitemap + robots.
- `hugo.yaml`: `theme: nowlin`, title "James Nowlin", trimmed to only
  params the theme uses. Menu gains **Hobbies**. PaperMod params removed.
- CSS is one Hugo-pipes bundle (`assets/css/main.css` + chroma),
  minified + fingerprinted with SRI.
- `/jnowlin.png` (about-page portrait) copied from `assets/images/` to
  `static/` so the URL resolves regardless of theme image pipelines.
  Lead images float right on desktop via a `:first-child` CSS rule;
  no content files were touched.
- Responsive at 860px breakpoint; single column, hamburger nav,
  stats stack. `prefers-reduced-motion` disables smooth scroll/transitions.

## Preserved

Every `.md` file under `content/` is byte-identical. All 20 aliases work.
URLs unchanged (`/about/`, `/posts/`, `/unt-mls/...`, `/hobbies/`).
Favicons, OG image, `robots.txt` layout override all still in place.

## Follow-ups (not done here)

- James mentioned more "reflections" from a Fall ePortfolio that could
  become blog posts. They live on jNix (unreachable from here); when he
  drops them into `content/posts/`, the blog list picks them up automatically.
- Cloudflare Pages builds with plain `hugo`; the new theme needs nothing
  beyond that. Recommend a quick visual pass on desktop + phone after deploy.
- `themes/papermod/` is dead weight now; delete it whenever (kept for rollback).
