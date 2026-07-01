# Exercise 1 - Hero section

- Wrapped both hero sections in a `.hero-group` flex container so they sit side by side on desktop and stack on mobile.
- Replaced the fixed pixel heights Luna's hero originally used (`960px` / `712px` / `490px` per breakpoint) with viewport units (`100dvh`, falling back to `100vh`), so the layout scales with the actual screen instead of a static number.
- Switched `background-size` to `cover` on both heroes, since fixed sizing only centered correctly at full viewport width and broke once the hero got split into columns.
- Added the new space section's background images to `overrides.css` following the same large/medium/small + retina breakpoint structure already used for Luna.
- Added the space.com link using the existing `.hero-link` class instead of wrapping headings in an `<a>`, with a visually hidden label so it isn't announced as unlabeled, plus `rel="noopener"` since it opens in a new tab.
- Capped hero copy with `max-width` and added `text-wrap: balance` so headlines wrap into short lines like the reference image, instead of stretching edge to edge.