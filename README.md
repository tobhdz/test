# Exercise 1 - Hero section

- Wrapped both hero sections in a `.hero-group` flex container so they sit side by side on desktop and stack on mobile.
- Replaced the fixed pixel heights Luna's hero originally used (`960px` / `712px` / `490px` per breakpoint) with viewport units (`100dvh`, falling back to `100vh`), so the layout scales with the actual screen instead of a static number.
- Switched `background-size` to `cover` on both heroes, since fixed sizing only centered correctly at full viewport width and broke once the hero got split into columns.
- Added the new space section's background images to `overrides.css` following the same large/medium/small + retina breakpoint structure already used for Luna.
- Added the space.com link using the existing `.hero-link` class instead of wrapping headings in an `<a>`, with a visually hidden label so it isn't announced as unlabeled, plus `rel="noopener"` since it opens in a new tab.
- Capped hero copy with `max-width` and added `text-wrap: balance` so headlines wrap into short lines like the reference image, instead of stretching edge to edge.

# Exercise 2 - Timeline ordering

- The bug was essentially an HTML grouping mistake rather than a CSS ordering issue. The original code grouped items 1-2-3 in one `col-lg-6` and 4-5-6 in another, causing a 1 4 / 2 5 / 3 6 reading sequence.
- I evaluated two approaches to fix this:
  - **Option A:** Give each card its own `col-12 col-lg-6` wrapper. While this immediately fixes the order, Bootstrap's default flex behavior stretches the rows and creates awkward dead space under shorter cards, breaking the dense masonry aesthetic.
  - **Option B (Chosen):** Keep the two original floating columns but interleave the items in the DOM (1, 3, 5 on the left; 2, 4, 6 on the right).
- Opting for the interleaving approach restores the correct left-to-right visual sequence while perfectly preserving the original masonry packing, as the columns flow independently. No CSS overrides were needed; fixing the HTML structure was the cleanest path.

# Exercise 3 - Gallery fallback for older browsers

- The gallery in `style.css` relies on `display: grid` with `grid-column` spans to lay out photos in 1/3, 2/3, and 1/2 pairs. Browsers without grid support (IE 11, older mobile webviews) get no layout at all and the photos just stack at full width without the intended proportions.
- Created a flexbox fallback that mimics the grid layout (`33.333%`, `66.667%`, `50%`), including `-ms-*` prefixes for IE10/11.
- Placed the fallback rules *outside* of any `@supports` block. If they were inside `@supports (not (display: grid))`, IE would discard the entire block since it doesn't recognize the `@supports` at-rule, defeating the purpose of the `-ms-*` prefixes. Modern browsers get their grid layout restored further down via `@supports (display: grid)`.
- Used the `flex: 0 0 X%` plus `max-width: X%` pattern for the columns to match Bootstrap's own `.col-*` implementation used elsewhere in the project. This prevents sub-pixel rounding issues and flex shrink edge-cases that can happen when using plain `width: X%`.
- Omitted the `.small-hide` mobile rule from the override since it already exists in `style.css` and its `display: none` behavior works independently of whether the parent is flex or grid.