# CLAUDE.md

Hugo static site for www.ianteda.com (personal blog/notes). Theme: `themes/proto`, in this repo; edit it directly.

## Commands

```bash
scripts/check                 # hugo build + front-matter lint (pre-commit hook and CI run this)
scripts/preview <slug>        # screenshots of a post at 1280 and 390 px, drafts included
scripts/publish [<bundle>] --trailer "Co-Authored-By: ..."   # go live: see Branches
hugo server --noHTTPCache --disableFastRender                 # dev server for Ian
```

Hugo is pinned in `mise.toml`, which CI also reads. There are no tests.

## Branches

Work happens on `drafts`. A post goes live only when `drafts` is merged into `main`, whose push triggers the deploy (`.github/workflows/build-and-deploy.yaml`). `scripts/publish <bundle>` does the whole thing: sets `draft: false`, commits, merges into `main` without a checkout, pushes, waits for the deploy, and curls the live URL. Without a bundle it ships everything already committed on `drafts`. Hugo skips posts dated in the future.

## Content

- Posts are page bundles: `content/<section>/YYYY-MM-DD-slug/index.md`, with their images alongside. New posts start from `archetypes/blog.md` with `draft: true`.
- URLs are `/<section>/<slug>/`, taken from the front matter `slug`, not the folder name. Use `aliases` when renaming.
- Taxonomies: `categories`, `series`, `tags`. Series pages live in `content/series/<name>/_index.md`.
- Menu entries are set in each section's `_index.md` front matter.

## Cover images

Every new blog post gets a cover: three concepts for Ian to choose from, then refinement. Follow `docs/agents/cover-image.md`.

## Agent docs

- Drafting a post from Ian's private knowledge base (Atlas): `docs/agents/atlas.md`. This repo is public, drafts included.
- Issue tracker (local markdown in `.scratch/<feature>/`): `docs/agents/issue-tracker.md`.
- Domain docs (`GLOSSARY.md`, `docs/adr/`): `docs/agents/domain.md`.
