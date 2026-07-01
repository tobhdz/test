# Exercise 1 - Hero section

- Wrapped both hero sections in a `.hero-group` flex container so they sit side by side on desktop and stack on mobile.
- Replaced the fixed pixel heights Luna's hero originally used (`960px` / `712px` / `490px` per breakpoint) with viewport units (`100dvh`, falling back to `100vh`), so the layout scales with the actual screen instead of a static number.
- Switched `background-size` to `cover` on both heroes, since fixed sizing only centered correctly at full viewport width and broke once the hero got split into columns.
- Added the new space section's background images to `overrides.css` following the same large/medium/small + retina breakpoint structure already used for Luna.
- Added the space.com link using the existing `.hero-link` class instead of wrapping headings in an `<a>`, with a visually hidden label so it isn't announced as unlabeled, plus `rel="noopener"` since it opens in a new tab.
- Capped hero copy with `max-width` and added `text-wrap: balance` so headlines wrap into short lines like the reference image, instead of stretching edge to edge.

# Exercise 2 - Timeline ordering

- The original markup grouped items 1–3 in one `col-lg-6` and 4–6 in another. On desktop the two columns sat side by side, so the visual reading order was 1 4 / 2 5 / 3 6 instead of the expected 1 2 / 3 4 / 5 6.
- Fixed it by giving each timeline card its own `col-12 col-lg-6` wrapper. Now flex-wrap on the `.row` naturally flows them in source order: two per row on large screens, one per row on mobile.
- Cleared `float: left` from `.timeline-item` in overrides since the original float is no longer needed once each card lives inside its own column, and it was preventing the cards from filling their container width.
- Considered a CSS Grid rewrite for the timeline container, but discarded it because the project already relies on Bootstrap's grid throughout, and introducing a second layout system for a fix this localized would add unnecessary complexity without any functional benefit.