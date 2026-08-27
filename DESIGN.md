# Design System — Purple/Paper Theme

## Color Tokens

### Primary Colors
- **Background**: `#faf7f1` — warm off-white paper, page background
- **Surface**: `#ffffff` — cards, table rows, secondary panels
- **Text**: `#1d1a1e` — primary text on light backgrounds
- **Divider**: `color-mix(in srgb, #1d1a1e 12%, transparent)`

### Accent — Deep Purple (primary CTA, kickers, links)
`--color-accent`: `#4a1942`. Tints/shades are derived from the base via `color-mix`, not a hand-authored ramp:
`100` `color-mix(in srgb, #4a1942 6%, white)` · `200` `color-mix(in srgb, #4a1942 14%, white)` · `300` `color-mix(in srgb, #4a1942 28%, white)` · `600` `color-mix(in srgb, #4a1942 85%, black)` · `700` `#4a1942` (base, used as the "700" text/heading tone)

### Accent 2 — Muted Gold (decorative hero blob, contact patch background)
`--color-accent-2`: `#8a6d2f`, added to pair with the purple since the source design referenced `--color-accent-2-100/200` without defining them:
`100` `color-mix(in srgb, #8a6d2f 8%, white)` · `200` `color-mix(in srgb, #8a6d2f 18%, white)` · `700` `color-mix(in srgb, #8a6d2f 85%, black)`

### Neutral
- `100` `#f2eee7` · `200` `#e9e3d8` · `800` `#3a3640` — used for neutral tags and secondary text tints (most other secondary text uses `color-mix(in srgb, var(--color-text) N%, transparent)` rather than a fixed neutral ramp).

## Typography

- **Headings**: Lora (Georgia fallback), weight 500 — an italic-capable serif that reads as editorial rather than corporate.
- **Body**: Inter, weights 400/500/600/700, loaded via Google Fonts (`https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,500;0,600;1,500&family=Inter:wght@400;500;600;700`).
- **Base size**: 15px, line-height 1.55. Hero H1 scales `clamp(38px, 5.4vw, 68px)`, section H2 `clamp(28px, 3vw, 40px)`.
- **Font hosting decision**: Google Fonts CDN, not self-hosted. The Organic theme self-hosted Caprasimo + Figtree deliberately — Caprasimo is a niche display font with no CDN fallback guarantee, so pinning it locally protected the brand voice and avoided a render-blocking third-party request for the one font carrying all the personality. Lora and Inter are both extremely widely used, heavily cached Google Fonts served from Google's edge network; the latency/reliability cost of the CDN is negligible for these two, and the source Design canvas export itself already wires up the Google Fonts `<link>` tags, so following that keeps the implementation aligned with the design source. Net: two different fonts, two different hosting calls, both deliberate.

## Spacing & Radius

- Scale: `--space-1` 4.4px through `--space-8` 35.2px (4.4px base unit) — unchanged from the prior theme; spacing scale is not theme-specific.
- Radius: `--radius-sm` 8px, `--radius-md` 16px (cards), `--radius-lg` 24px (hero image panel). Buttons are **not** pill-shaped in this theme — `.btn` uses `border-radius: 10px`, a deliberate departure from the Organic theme's full-pill buttons. Tags remain pill-shaped (`999px`).

## Elevation

- `--shadow-sm` / `--shadow-md` / `--shadow-lg` — soft ink-tinted shadows (`color-mix` against `#1d1a1e`), no hard black shadows.

## Component Patterns

### Navigation
- Sticky top nav, translucent paper background with `backdrop-filter: blur(6px)`. Links: Leadership, Experience, Projects, Credentials, Contact, plus a solid-purple `.btn-primary` LinkedIn button as the CTA (replacing the Organic theme's "Email me" nav CTA).

### Hero
- Two-column grid: headline + copy + CTA row on the left, an image collage panel on the right (`border-radius: 24px`, `shadow-lg`) with a decorative gold-tinted circle bleeding off the top-right corner behind it, and a floating "Cumulative savings — $20M+" stat card overlapping its bottom-left corner.
- Hero image is a real asset (`assets/img/hero-collage.webp`): a dark-mode collage of a model-training/data-pipeline diagram, a fulfillment metrics table, a rising line chart, plus a purple US logistics network map with truck/air routes between hubs.

### Leadership Approach
- New section (not present in the prior Organic theme): a 2×2 grid of labeled percentage progress bars (`.progress-track` / `.progress-fill`), each with a title, a percentage in the heading font, and a one-line description underneath.

### Career-Highlight Stat Strip
- 4-column strip bordered top/bottom by `--color-divider`, with a vertical divider between each of the first three columns. Each column: a small icon square (`--color-accent-100` background, 6px radius) beside a large heading-font value, with a label line below. Replaces the Organic theme's circular stat tiles.

### Cards
- `.card` — white surface, `1px solid var(--color-divider)` border, `16px` radius, `28px 32px` padding, `--shadow-sm`. Border is new; the Organic theme's cards had no border and relied purely on elevation.
- Project cards lift on hover (`translateY(-4px)` + `--shadow-lg`), same interaction as before.
- Project cards with a real still image show it as a top-bleed panel (`18px` radius, negative margin to bleed to the card edges) above the kicker/title/body.

### Buttons
- `.btn-primary` — solid purple fill, white text.
- `.btn-secondary` — white fill, divider-color border.
- `.btn-ghost` — text-only accent, used for "view all" style links.
- All non-pill, `10px` radius (see Radius above).

### Tags
- Pill-shaped, 11px. `.tag-neutral` / `.tag-accent-2` for filled variants, `.tag-outline` for outlined (used on project cards). `.tag-accent-2` uses the purple 100/700 tones (matching the source design's actual CSS, despite the class name), while the new gold `--color-accent-2` tokens are reserved for backgrounds/decoration.

## Motion

- `revealUp`, `heroFade` on section/hero entrance — unchanged mechanism from the prior theme.
- All animation disabled under `prefers-reduced-motion: reduce`; `html { scroll-behavior: smooth }` for anchor nav, also disabled under reduced motion.

## Accessibility

- Text/background contrast: `#1d1a1e` on `#faf7f1` exceeds WCAG AAA.
- `:focus-visible` gets a 2px accent outline; default `:focus` is suppressed only where a visible alternative exists.
- Semantic landmarks: `<nav>`, `<section id="...">` per content block, heading hierarchy h1 → h2 → h3.
- All new `<img>` elements carry descriptive `alt` text (hero collage, and the 3 project thumbnails).

## Responsive

- Single breakpoint at 800px: hero grid, leadership grid, stats grid, projects grid, stack education/certifications columns, and the contact panel all collapse to one column; hero visual drops to full width below the copy.

## Font Fallback Chain

```
Headings: Lora, Georgia, serif
Body:     Inter, system-ui, sans-serif
```

## Real Images

- `assets/img/hero-collage.webp` — hero visual (decoded from the Design canvas's embedded image-slot data).
- `assets/img/proj-1.webp` — Multi-Agent Merchant Education Pipeline card ("Initial Assessment → Curriculum Generation → Agent Delivery → Performance Tracking" workflow).
- `assets/img/proj-2.webp` — Warehouse Ops Intelligence card ("Weekly Operations Dashboard": warehouse network graph + weekday bar charts).
- `assets/img/proj-3.webp` — Chargeback RCA Framework card ("Sparse Causal Graph" + "Descending Defect Trend Chart").

---

**Version**: 3.0
**Last Updated**: August 26, 2026
**Theme**: Purple/Paper (imported from a new Claude Design canvas export — "Arjun Kulshreshtha Portfolio")
