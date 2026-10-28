# Atlas: drafting posts from Ian's knowledge base

Atlas (`~/Projects/Atlas`) is Ian's private knowledge base: a wiki compiled from his books, articles, notes and records. This repo reads it and never writes to it. Everything here is public: the site, and the repo on GitHub, drafts included. `draft: true` keeps a post off the site, not out of the repo.

## Find what Atlas knows

1. Read `~/Projects/Atlas/90-Knowledge/index.md`. It has one line per page, and at Atlas's size it is the retrieval layer.
2. Search by keyword. qmd is pinned in Atlas's `mise.toml`, not here, so a bare `qmd` fails:

   ```bash
   mise -C ~/Projects/Atlas exec -- qmd search -c knowledge "<keywords>"
   ```

   It ANDs every term and its score is no threshold, so search keywords, not sentences. Never `qmd query` or `qmd vsearch`: they take minutes on this hardware. A result `qmd://knowledge/<path>` is the file `~/Projects/Atlas/90-Knowledge/<path>`.
3. Read the pages. `10-Concepts/` pages synthesise across sources; `00-Sources/src--<author>--<title>.md` pages summarise one source each, with `author` and `published` in the frontmatter. `[[wikilinks]]` name other pages in the same tree.

## What a post may draw on

Only `90-Knowledge/`. Never read `10-Cabinet/`, `01-Notes/`, `99-Memory/` or `30-Projects/`; the Cabinet holds raw captures with Ian's details unredacted. One exception: a source page's `capture:` link names a Cabinet file, and its frontmatter `source_url` may be read to link the original publicly.

Even inside `90-Knowledge/`, keep these out of a post unless Ian names them for that post:

- health: blood results, heart rate, sleep, training data
- money: payments, ledgers, loan and mortgage figures, prices Ian paid or offered
- property: addresses, listings, agents, inspections
- people other than Ian (pages in `30-People/` are mostly public authors, but not all), and Ian's family
- GHD, Sydney Water, or any work engagement
- Atlas's own build history: session pages (`src--atlas-bootstrap--…` and any `src--` page dated with a hash suffix)
- machines, accounts, email addresses, homelab hosts

Other people's published ideas are fair to use. Credit the author and work, and link the public original, never Atlas.

## Draft

1. Agree the angle with Ian if he hasn't given one: one post, one idea.
2. Read two or three posts in `content/blogs/` for Ian's voice. Write in Australian English.
3. Create `content/blogs/YYYY-MM-DD-slug/index.md` with front matter from `archetypes/blog.md`: `draft: true`, `slug` set explicitly, tags in Title Case as existing posts use them.
4. No wikilinks, Atlas paths or Atlas page names in the post.

## Privacy check, then hand over

Before calling a draft done, report in chat (not in the post):

- the Atlas pages used, by path
- every fact in the draft about Ian or someone he knows, each for Ian to keep or cut
- the result of this check, which must print nothing:

  ```bash
  rg -n '\[\[|~/Projects|90-Knowledge|10-Cabinet|01-Notes|99-Memory|src--' content/blogs/<bundle>/
  ```

Do not commit a draft until Ian has cleared the list: a commit is public once pushed, and a push to `main` deploys the site.
