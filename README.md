# ianteda.com

Hugo source for www.ianteda.com. Theme: `themes/proto`.

```bash
git config core.hooksPath .githooks             # once per clone: run scripts/check before each commit
hugo server --noHTTPCache --disableFastRender   # dev server
scripts/check                                   # build + front-matter lint
scripts/preview <slug>                          # screenshot a post
scripts/publish [content/<section>/<bundle>]    # merge drafts into main and deploy
```

See `CLAUDE.md` for the branch model and content conventions.

## Figure shortcode

```md
{{< figure src="image-in-bundle.jpg" link="https://..." attr="Figure title" class="align-center" attrlink="https://..." >}}
```

## Legacy photo covers

Posts before 2026 reference `/images/covers/cover-*.png`, produced from `src/cover-images/` by `npm ci && npx gulp`. The proto theme does not display them; new covers live in the post bundle.
