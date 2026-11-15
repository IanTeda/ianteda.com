# Cover image

Ian picks every cover. Draft three concepts, let him choose, then refine the one he chose.

## House style

Read one of these before drafting; they are the style source of truth:

- `content/blogs/2026-11-10-building-personal-ledger-with-ai/ai-assistant-roles.svg` (diagram)
- `content/blogs/2026-11-03-personal-ledger-keyboard-navigation/personal-ledger-keyboard.svg` (product mockup)

The rules they share:

- Hand-written SVG, `viewBox="0 0 1200 562"`, rendered at 2x to a 2400×1124 PNG.
- `font-family="Archivo, 'Liberation Sans', 'Helvetica Neue', Arial, sans-serif"`. Archivo is not installed locally, so renders use Liberation Sans. Check the PNG for text overflow.
- Background `#f2f2f2` or `#fff`, ink `#1d1d1b`, greys `#5a5a5a` `#8a8a8a` `#c4c4c4`. At most one accent, red `#ee3a1c`.
- Flat, editorial, monochrome: boxes, keys, arrows, a few words. No gradients, no shadows, no photos.
- Personal Ledger posts use the Personal Ledger mockup style (the keyboard cover and the `keyboard-mockup` shortcode).
- A `<title>` element describes the image.

## Steps

1. **Read the post.** Find the one idea a reader should see at a glance.
2. **Draft three concepts**, each a different angle on that idea (for example: a diagram, a product mockup, a metaphor). Write them to `$TMPDIR/cover/a.svg`, `b.svg` and `c.svg`.
3. **Render a contact sheet.** One image read, not three:

   ```bash
   cd $TMPDIR/cover
   for x in a b c; do rsvg-convert -w 1200 $x.svg -o $x.png; done
   magick montage a.png b.png c.png -tile 1x3 -geometry 1000x+0+24 -label '%t' -pointsize 28 sheet.png
   ```

   Read `sheet.png` yourself. Fix any clipped or overlapping text before showing Ian.
4. **Present it.** Show Ian the full path to `sheet.png` and one line per concept. Ask which one he wants and what to change. Stop here until he answers.
5. **Refine** the chosen SVG until he signs off. Re-render it at 1200 px wide for each review.
6. **Install it** in the post's bundle at `content/<section>/<bundle>/`:

   ```bash
   rsvg-convert -w 2400 <name>.svg -o <name>.png
   magick <name>.png -strip <name>.png
   ```

   Commit both the `.svg` and the `.png`, then set the front matter:

   ```yaml
   cover:
     image: <name>.png
     caption: "..."
     alt: "..."
     style: full
   ```

   The theme shows only a cover image that sits in the page bundle. A `/images/covers/...` path is silently skipped. `scripts/check` fails if the file is missing.
7. **Show it in place.** Run `scripts/preview <slug>`.

Done when Ian has approved the image in the preview.
