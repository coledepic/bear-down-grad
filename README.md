# Bear Down, We're Graduating

Kylie & Austin's UArizona 2027 graduation invite site.

**It is one site, not three.** All three URLs serve identical content in a single continuous
scroll (hero → RSVP → details). The only difference is that the two personal links open with a
full-screen intro overlay spotlighting that graduate, which dismisses into the same shared site:

| Link | What's different |
|---|---|
| `/` | No overlay — the plain shared site. Send to people who know them both. |
| `/kylie/` | Opens with Kylie's intro overlay, then the same site. |
| `/austin/` | Opens with Austin's intro overlay, then the same site. |

The overlay shows once per browsing session (tracked in `sessionStorage`). Add `?intro` to any
personal link to force it to show again when previewing — e.g. `/kylie/?intro`.

Separate routes (rather than one page with a `?for=` parameter) exist so each link can carry its
own iMessage/social preview image and title — crawlers read static HTML per URL.

Earlier versions are preserved as git tags: `v1-mockup-rebuild` (the itinerary-style first pass).

## Before sending this out

1. **Add real photos.** See `public/images/README.md` for exact filenames — drop photos in, no
   code changes needed. Until then, hero/intro/grad-card spots show a navy gradient (not a broken
   image). The design leans hard on these, so it will look markedly better once they're in.
2. ~~Turn on the RSVP form.~~ Done — it posts to Formspree form `xzebpgyj`. Submissions land in
   the Formspree dashboard + notification email. Nothing is stored by this site itself.
3. **Wire up the real map.** See "The map" section in `public/images/README.md` — needs a quick
   Google My Maps setup (free, ~5 minutes) since a plain embed only supports one pin.
4. **Fill in what's still TBD** — Saturday's party time (`src/components/Details.astro`), and an
   RSVP deadline / contact line if you want them (the `contactLine` prop, passed from each page
   file into `BaseLayout`).

## Editing

- **All the detail sections** (graduates, celebration, stay, travel, things to do, map, FAQ) —
  `src/components/Details.astro`. Edit once, it updates everywhere.
- **Hero** (headline, welcome line, date pills) — `src/components/Hero.astro`. Shared by all three
  URLs, since it's one site.
- **The personal intro overlays** — `src/components/PersonaIntro.astro` for behavior/markup; the
  per-person name, degree, message and photo are props passed from `src/pages/kylie.astro` and
  `src/pages/austin.astro`.
- **RSVP form fields** — `src/components/RsvpPanel.astro`.
- **Header/footer, meta + OG tags, the countdown** — `src/layouts/BaseLayout.astro`.
- **Icons** — `src/components/Icon.astro`, a small hand-authored stroke set (no icon library).
  Add new ones in the same style; use `<Icon name="..." />`.
- **Colors/fonts/spacing/animations** — `src/styles/global.css` (mobile-first: base rules target
  small screens, `@media (min-width: ...)` blocks layer on tablet/desktop enhancements).

Everything respects `prefers-reduced-motion` — the marquee, scroll reveals, countdown ticks and
confetti all disable for visitors who ask for reduced motion.

## Local development

```sh
npm install
npm run dev
```

Opens at `http://localhost:4321/bear-down-grad/` (the `/bear-down-grad/` base path matches the
GitHub Pages project URL — see `astro.config.mjs`).

```sh
npm run build      # builds to ./dist
npm run preview    # preview the production build locally
```

## Deploying (GitHub Pages)

This repo already has a GitHub Actions workflow (`.github/workflows/deploy.yml`, already fixed
for Node 22) that builds and deploys on every push to `main`. GitHub Pages is already enabled
(Settings → Pages → Source → GitHub Actions) — just push, and the site publishes to
`https://coledepic.github.io/bear-down-grad/`.

If you ever move to a custom domain, update `site`/`base` in `astro.config.mjs`, update the
hardcoded `coledepic.github.io` URLs in `src/layouts/BaseLayout.astro` (used for OG/canonical
tags), and add a `CNAME` file in `public/`.
