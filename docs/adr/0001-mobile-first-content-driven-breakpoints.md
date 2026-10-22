# Mobile-first, content-driven breakpoints

The redesign is written mobile-first: the unqueried CSS is the layout for a 320px viewport with 16px gutters, and larger tiers only add to it through `min-width` queries. There are three tiers: mobile (base), tablet (`40em`), desktop (`60em`). They sit where the content needs them, not at device widths, and they are in `em` so they follow the reader's font size. Body text keeps a `65ch` measure in every tier and page chrome stops at about 1080px. Type and spacing scale fluidly with `clamp()`, so breakpoints only change layout.

## Considered Options

- **Device-width breakpoints (375/768/1024px)**: rejected. Devices keep changing, while the measure of a reading site does not.
- **Breakpoint tokens through a CSS build step (Sass/PostCSS custom media)**: rejected. With only two values, plain literals and one comment that documents them are enough.

## Consequences

- The tier names (mobile/tablet/desktop) are only labels for width ranges. Nothing detects devices.
- Page layout uses media queries. Container queries are only for components that appear at several widths.
- The desktop tier changes chrome only. A sidebar or table of contents beside the article would be a new decision.
- Exception: the home page intro (the text and cover photo above the recent list) is not held to the measure. It spans the full chrome width so it lines up with the post list below it. On desktop that is about 110 characters per line, which we accept on this one page because a matching layout matters more there. Posts keep the measure.
