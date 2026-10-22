# Mobile-first, content-driven breakpoints

The redesign is written mobile-first: the unqueried CSS is the layout for a 320px viewport with 16px gutters, and larger tiers only add to it through `min-width` queries. There are three tiers: mobile (base), tablet (`40em`), desktop (`60em`). They sit where the content needs them, not at device widths, and they are in `em` so they follow the reader's font size. Page chrome stops at about 1080px, and body text spans that full width in every tier, on posts as well as the home page. From the tablet tier up, articles and everything on the home page (header, intro, post list and sections) are inset by a `5ch` margin on each side, so they sit inside the nav and footer. Type and spacing scale fluidly with `clamp()`, so breakpoints only change layout.

## Considered Options

- **Device-width breakpoints (375/768/1024px)**: rejected. Devices keep changing, while the measure of a reading site does not.
- **Hold posts to a `65ch` measure**: tried first, then dropped. Posts were narrower than the home page, so the column changed width between pages.
- **Breakpoint tokens through a CSS build step (Sass/PostCSS custom media)**: rejected. With only two values, plain literals and one comment that documents them are enough.

## Consequences

- The tier names (mobile/tablet/desktop) are only labels for width ranges. Nothing detects devices.
- Page layout uses media queries. Container queries are only for components that appear at several widths.
- The desktop tier changes chrome only. A sidebar or table of contents beside the article would be a new decision.
- Superseded: the home page and posts were first different. Posts kept a `65ch` measure and only the home page intro spanned the chrome width. Now every page spans the chrome width so the main column is the same width across the site. On desktop that is about 110 characters per line. We accept that longer measure because a consistent column matters more to us than the shorter line length.
