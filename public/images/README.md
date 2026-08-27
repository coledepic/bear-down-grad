# Photos go here

Drop in real photos with these exact filenames and the site will pick them up automatically
(no code changes needed). Until a file exists, that spot just shows a navy gradient — it won't
break or show a broken-image icon.

| Filename | Used for | Suggested size |
|---|---|---|
| `hero-duo.jpg` | Full-bleed hero background on the combined (`/`) page | 1600×2000 or larger, portrait works well on mobile |
| `hero-kylie.jpg` | Full-bleed hero background on Kylie's page (`/kylie/`) | 1600×2000 or larger |
| `hero-austin.jpg` | Full-bleed hero background on Austin's page (`/austin/`) | 1600×2000 or larger |
| `grad-kylie.jpg` | Kylie's card in "Meet the Graduates" | 1200×900 or larger |
| `grad-austin.jpg` | Austin's card in "Meet the Graduates" | 1200×900 or larger |
| `og-duo.jpg` | The iMessage/social link-preview image for `/` | exactly 1200×630 |
| `og-kylie.jpg` | The iMessage/social link-preview image for `/kylie/` | exactly 1200×630 |
| `og-austin.jpg` | The iMessage/social link-preview image for `/austin/` | exactly 1200×630 |

The hero photos sit behind a gradient that's darkest at the bottom (where the text is) and clear
at the top, so the photo itself stays the visual focus — pick something that reads well with the
top portion left uncluttered by text/faces if possible. The `og-*` images are what shows up when
the link is pasted into iMessage/WhatsApp/etc. — they can just be a nicely cropped version of the
matching hero photo at 1200×630.

## The map (needs a 5-minute manual step)

The Map section needs pins for: University of Arizona (campus), The Mark Tucson (the party — 55 N
Park Ave, Tucson, AZ 85719), TUS airport, PHX airport, major hotel areas, University Blvd, 4th
Ave, Mt. Lemmon, and Casino Del Sol Stadium (545 N National Champion Dr — commencement). A plain
Google Maps embed only supports one pin, so the real multi-pin map needs a **Google My Maps**
(free, no API key, no billing):

1. Go to [mymaps.google.com](https://mymaps.google.com), sign in, "Create a new map."
2. Add each location above as a pin (search it, click "Add to map"), rename each pin to something
   short and clear (e.g. "The Party 🏠", "Commencement 🎓").
3. Map → Share → make it public ("Anyone with the link can view").
4. Map menu (⋮) → **Embed on my site** → copy the `<iframe src="...">` URL.
5. Paste that URL into `MAP_EMBED_SRC` in `src/components/DetailsView.astro` (near the top,
   clearly marked with a comment).

Until that's done, the Map section shows a placeholder single-pin embed (just The Mark Tucson) so
the page isn't broken — but it won't show the full pin set until the real one is wired in.
