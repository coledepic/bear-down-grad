# Bear Down, We Graduated 🎓

Kylie & Austin's UArizona 2027 graduation invite site. Three shareable landing pages, each an
**Invite · RSVP** view (default) with a **Details** view one tap away via the sticky toggle in
the header:

- `/` — combined page (for people who know both of them)
- `/kylie/` — Kylie's personal page
- `/austin/` — Austin's personal page

v1 (the itinerary-style rebuild of the original mockup) is preserved at the git tag
`v1-mockup-rebuild` if you ever want to look back at it (`git show v1-mockup-rebuild:README.md`,
or `git checkout v1-mockup-rebuild` to browse it fully).

## Before sending this out

1. **Add real photos.** See `public/images/README.md` for exact filenames — drop photos in, no
   code changes needed. Until then, hero/grad-card spots show a navy gradient (not a broken
   image).
2. **Turn on the RSVP form.** It posts to [Formspree](https://formspree.io) (free — no backend,
   no database, responses land in your email + a Formspree dashboard/CSV export).
   - Sign up free at formspree.io, create a new form.
   - Copy your form ID (`https://formspree.io/f/XXXXXXXX` — the `XXXXXXXX` part).
   - Open `src/components/RsvpPanel.astro`, find `const FORMSPREE_ID = 'YOUR_FORM_ID';` near the
     top, paste your real ID in. One shared component, one edit covers all three pages.
3. **Wire up the real map.** See "The map" section in `public/images/README.md` — needs a quick
   Google My Maps setup (free, ~5 minutes) since a plain embed only supports one pin.
4. **Fill in what's still TBD** — Saturday's party time (`src/components/DetailsView.astro`), and
   an RSVP deadline / contact info if you want them (footer `contactLine` prop, passed from each
   page file).

## Editing

- **Shared Details content** (graduates, celebration, stay, travel, things to do, map, FAQ) — all
  in `src/components/DetailsView.astro`. Edit once, it updates on all three pages.
- **RSVP form fields** — `src/components/RsvpPanel.astro`.
- **Personalized hero** (headline, welcome line, background photo) — in each page file:
  `src/pages/index.astro`, `src/pages/kylie.astro`, `src/pages/austin.astro`, via props passed to
  `<Hero>`.
- **Header/footer, the Invite↔Details toggle, meta/OG tags, the countdown** —
  `src/layouts/BaseLayout.astro`.
- **Colors/fonts/spacing/animations** — `src/styles/global.css` (mobile-first: base rules target
  small screens, `@media (min-width: ...)` blocks layer on tablet/desktop enhancements).

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
