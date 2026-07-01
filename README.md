# Exercise 1 - Hero section

- Wrapped both hero sections in a `.hero-group` flex container so they sit side by side on desktop and stack on mobile.
- Replaced the fixed pixel heights Luna's hero originally used (`960px` / `712px` / `490px` per breakpoint) with viewport units (`100dvh`, falling back to `100vh`), so the layout scales with the actual screen instead of a static number.
- Switched `background-size` to `cover` on both heroes, since fixed sizing only centered correctly at full viewport width and broke once the hero got split into columns.
- Added the new space section's background images to `overrides.css` following the same large/medium/small + retina breakpoint structure already used for Luna.
- Added the space.com link using the existing `.hero-link` class instead of wrapping headings in an `<a>`, with a visually hidden label so it isn't announced as unlabeled, plus `rel="noopener"` since it opens in a new tab.
- Capped hero copy with `max-width` and added `text-wrap: balance` so headlines wrap into short lines like the reference image, instead of stretching edge to edge.

# Exercise 2 - Timeline ordering

- The original markup grouped items 1–3 in one `col-lg-6` and 4–6 in another. Two columns side by side gave a 1 4 / 2 5 / 3 6 reading order instead of the 1 2 / 3 4 / 5 6 the brief's own diagram shows.
- First try was keeping the masonry-style packing by interleaving the DOM and reordering with CSS for mobile. Dropped it once I noticed the brief's diagram is fixed row pairs, not independent columns, so masonry was never the goal.
- Real masonry with guaranteed left-to-right order isn't something CSS does well on its own, and JS is off the table per the brief. Went with one `col-12 col-lg-6` per card in plain source order instead; flex-wrap on the row handles two per row on desktop and one per row on mobile with no extra logic.
- Cleared `float: left` from `.timeline-item`, left over from when cards shared a column, since it was keeping cards from filling their new wrapper.
- Cards of different lengths don't line up at the bottom within a row. Left it alone to keep the card style untouched, per the extra points.

# Exercise 3 - Gallery fallback for older browsers

- The gallery in `style.css` relies on `display: grid` with `grid-column` spans to lay out photos in 1/3, 2/3, and 1/2 pairs. Browsers without grid support (IE 11, older mobile webviews) get no layout at all and the photos just stack at full width without the intended proportions.
- Created a flexbox fallback that mimics the grid layout (`33.333%`, `66.667%`, `50%`), including `-ms-*` prefixes for IE10/11.
- Placed the fallback rules *outside* of any `@supports` block. If they were inside `@supports (not (display: grid))`, IE would discard the entire block since it doesn't recognize the `@supports` at-rule, defeating the purpose of the `-ms-*` prefixes. Modern browsers get their grid layout restored further down via `@supports (display: grid)`.
- Used the `flex: 0 0 X%` plus `max-width: X%` pattern for the columns to match Bootstrap's own `.col-*` implementation used elsewhere in the project. This prevents sub-pixel rounding issues and flex shrink edge-cases that can happen when using plain `width: X%`.
- Omitted the `.small-hide` mobile rule from the override since it already exists in `style.css` and its `display: none` behavior works independently of whether the parent is flex or grid.