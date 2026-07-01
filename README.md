# Exercise 1 - Hero section

- Wrapped both hero sections in a flex container so they sit side by side on desktop and stack on mobile.
- Replaced the fixed pixel height Luna's hero originally used (`960px` / `712px` / `490px` per breakpoint) with viewport-based height (`vh`, with a `dvh` fallback) for both heroes, so the layout scales with the actual screen instead of a static number.
- Switched `background-size` from fixed pixels to `cover` on both heroes, since fixed sizing only centers correctly at full viewport width and breaks once the hero is split into columns.
- Kept the large/medium/small + retina breakpoint structure already used for Luna's images, applied the same way to the new space section's assets.
- Added the space.com link using the existing `.hero-link` class instead of wrapping headings in an `<a>`, with a visually hidden text label so the link isn't announced as unlabeled by screen readers.
- Capped hero copy width with `max-width` and added `text-wrap: balance` so headline text wraps into short lines (as showed in the expected reference image) instead of stretching edge to edge.
