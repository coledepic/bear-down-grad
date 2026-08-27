# Bear Down, We Graduated 🎓

Kylie & Austin's UArizona 2027 graduation weekend site. Three pages, one shared set of
weekend/logistics content:

- `/` — combined page (both grads)
- `/kylie/` — personalized page for Kylie, same shared content below the hero
- `/austin/` — personalized page for Austin, same shared content below the hero

## Before sending this out

1. **Add real photos.** See `public/images/README.md` for exact filenames — drop photos in,
   no code changes needed. Until then, hero/grad-card spots show a navy/red gradient (not a
   broken image).
2. **Turn on the RSVP form.** It posts to [Formspree](https://formspree.io) (free — no backend,
   no database, responses land in your email + a Formspree dashboard/CSV export).
   - Sign up free at formspree.io, create a new form.
   - Copy your form ID (Settings → your form → "Integration" shows the endpoint,
     `https://formspree.io/f/XXXXXXXX` — the `XXXXXXXX` part is the ID).
   - Open `src/components/SharedContent.astro`, find `const FORMSPREE_ID = 'YOUR_FORM_ID';`
     near the top, and paste your real ID in.
   - Since the RSVP section is in the one shared component, this only needs doing once —
     it applies to all three pages.
3. **Double-check the details** — Saturday's party time is still TBD in the copy
   (`src/components/SharedContent.astro`), and the countdown target date/time is set in
   `src/layouts/BaseLayout.astro` (`new Date("2027-05-14T19:30:00-07:00")`).

## Editing

- **Shared content** (weekend schedule, hotels, travel, party, things to do, map, RSVP, FAQ) —
  all in `src/components/SharedContent.astro`. Edit once, it updates on all three pages.
- **Personalized bits** (name, headline, intro blurb, background photo) — in each page file:
  `src/pages/index.astro`, `src/pages/kylie.astro`, `src/pages/austin.astro`.
- **Colors/fonts/layout** — `src/styles/global.css`.

## Local development

```sh
npm install
npm run dev
```

Opens at `http://localhost:4321/bear-down-grad/` (the `/bear-down-grad/` base path matches
the GitHub Pages project URL — see `astro.config.mjs`).

```sh
npm run build      # builds to ./dist
npm run preview    # preview the production build locally
```

## Deploying (GitHub Pages)

This repo already has a GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds
and deploys on every push to `main`. One-time setup on GitHub:

1. Push this repo to GitHub (if not already).
2. Repo → **Settings → Pages → Source → GitHub Actions**.
3. Push to `main` (or re-run the workflow) — the site publishes to
   `https://coledepic.github.io/bear-down-grad/`.

If you ever move to a custom domain, update `site`/`base` in `astro.config.mjs` and add a
`CNAME` file in `public/`.
