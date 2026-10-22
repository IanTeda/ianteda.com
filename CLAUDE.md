# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Hugo static site for www.ianteda.com (personal blog/notes), using the [Minimo](https://github.com/MunifTanjim/minimo) theme as a git submodule at `themes/minimo` (clone with `--recurse-submodules`). Deployed to GitHub Pages by `.github/workflows/hugo.yaml` on every push to `main`.

## Commands

```bash
hugo server --noHTTPCache --disableFastRender   # dev server
hugo --gc --minify                              # production build (what CI runs) -> ./public
npm ci && npx gulp                              # regenerate cover images
```

- CI pins **Hugo extended 0.168.0** (pinned for local use in `mise.toml`; keep both in sync).
- There are no tests or linters (`npm test` is a stub).
- `gulp` (default task `coverImage`) resizes/crops every `src/cover-images/*.{jpg,png}` to 1200x562, compresses, and writes PNGs to `static/images/covers/`. Put source photos in `src/cover-images/` and reference the output as `/images/covers/cover-<name>.png`. Other `gulpfile.mjs` tasks are commented out.

## Architecture

- **Config** is split in `config/_default/` (`config.toml`, `params.toml`, `menu.toml`). Menu entries are *not* in `menu.toml` (it is commented out); they are set in each section's `_index.md` front matter.
- **Content** (`content/`) is organised in sections: `blogs`, `notes`, `engineering-rule-book`, `letters-to-my-sons`, plus single pages (`now`, `contact`, `page/search.md`). Posts are page bundles: `content/<section>/YYYY-MM-DD-slug/index.md` with images/attachments alongside.
- **Permalinks**: `[permalinks] page = "/:slug/"`, so the URL comes from the front matter `slug`, not the folder name. Set `slug` explicitly and use `aliases` when renaming.
- **Taxonomies**: `categories`, `series`, `tags`. Series pages live in `content/series/<name>/_index.md` (e.g. the Engineering Rule Book rules belong to a series of that name).
- **Overrides of the theme** live in the root `layouts/` (`partials/head/analytics.html`, `shortcodes/download.html`) and `static/`; never edit `themes/minimo`.
- **Archetypes** (`archetypes/`): `default.md`, `blog.md`, `post.md`. The default archetype documents the full front-matter set, including the Minimo `cover:` block (`image`, `caption`, `style`). New content is created with `draft: true`.
- Syntax highlighting uses Pygments-style code fences (`pygmentsCodefences`); the `figure` shortcode is used for images with links/attribution (see `README.md`).

## Agent skills

### Issue tracker

Issues are local markdown files under `.scratch/<feature>/`. See `docs/agents/issue-tracker.md`.

### Domain docs

Single-context: one `GLOSSARY.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
