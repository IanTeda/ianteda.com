# Cover image

Ian picks every cover. Draft three concepts, let him choose, then refine the one he chose.

## House style

Read one of these before drafting; they are the style source of truth:

- `content/blogs/2026-11-10-building-personal-ledger-with-ai/ai-assistant-roles.svg` (diagram)
- `content/blogs/2026-11-03-personal-ledger-keyboard-navigation/personal-ledger-keyboard.svg` (product mockup)
- `content/blogs/2026-11-17-personal-ledger-viper/personal-ledger-viper-cover.svg` (photo with legend)

The rules they share:

- Hand-written SVG, `viewBox="0 0 1200 562"`, rendered at 2x to a 2400×1124 PNG.
- `font-family="Archivo, 'Liberation Sans', 'Helvetica Neue', Arial, sans-serif"`. Archivo is not installed system-wide: render with the real font (see Rendering with Archivo), not the Liberation Sans fallback. Check the PNG for text overflow.
- Background `#f2f2f2` or `#fff`, ink `#1d1d1b`, greys `#5a5a5a` `#8a8a8a` `#c4c4c4`. At most one accent: the site's green `#1a7f37` (light-theme `--green` in `themes/proto/static/proto/site.css`), or red `#ee3a1c` to match the older diagrams.
- Flat, editorial, monochrome: boxes, keys, arrows, a few words. No gradients, no shadows.
- Photos only when Ian asks for one: greyscale, public domain or CC-licensed (Wikimedia Commons is a good source), embedded in the SVG as base64 so the file stands alone, and credited in the cover `caption` (photographer, source, licence) even when public domain.

## Rendering with Archivo

Download Archivo into `$TMPDIR` once and point fontconfig at it for every `rsvg-convert` call:

```bash
mkdir -p $TMPDIR/fonts $TMPDIR/fc
curl -sL -o $TMPDIR/fonts/Archivo.ttf "https://github.com/google/fonts/raw/main/ofl/archivo/Archivo%5Bwdth%2Cwght%5D.ttf"
printf '<?xml version="1.0"?><!DOCTYPE fontconfig SYSTEM "fonts.dtd"><fontconfig><include ignore_missing="yes">/etc/fonts/fonts.conf</include><dir>%s/fonts</dir><cachedir>%s/fc/cache</cachedir></fontconfig>\n' "$TMPDIR" "$TMPDIR" > $TMPDIR/fc/fonts.conf
export FONTCONFIG_FILE=$TMPDIR/fc/fonts.conf
fc-list | grep -qi archivo && echo "Archivo found"
```
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
