# Design System — Organic Theme

## Color Tokens

### Primary Colors
- **Background**: `#f5ead8` — warm cream, page background
- **Surface**: `#ebddc5` — cards, table rows, secondary panels
- **Text**: `#201e1d` — primary text on light backgrounds
- **Divider**: `color-mix(in srgb, #201e1d 16%, transparent)`

### Accent — Terracotta (primary CTA, kickers, links)
`100` `#fff2eb` · `200` `#ffe1d0` · `300` `#ffc6a5` · `400` `#f6a06b` · `500` `#d67f48` (`--color-accent`: `#c67139`) · `600` `#b2622d` · `700` `#8c491a` · `800` `#643312` · `900` `#402310`

### Accent 2 — Olive (secondary stats, education tags)
`100` `#f0fae1` · `200` `#e1eecc` · `300` `#ccdbb2` · `400` `#aebf92` · `500` `#8fa073` (`--color-accent-2`: `#7a8a5e`) · `600` `#728157` · `700` `#56633f` · `800` `#3d472b` · `900` `#272e1b`

### Neutral Ramp
`100` `#f9f4ed` · `200` `#eee7db` · `300` `#dcd3c4` · `400` `#c0b6a5` · `500` `#a19786` · `600` `#82796a` · `700` `#645c50` · `800` `#474238` · `900` `#2e2b25`

## Typography

- **Headings**: Caprasimo (system-ui fallback), weight 400 only — the display font carries the personality, so headings never go bold.
- **Body**: Figtree, weights 400/600/700.
- **Base size**: 15px, line-height 1.55. Hero H1 scales `clamp(38px, 5.4vw, 68px)`, section H2 `clamp(28px, 3vw, 40px)`.

## Spacing & Radius

- Scale: `--space-1` 4.4px through `--space-8` 35.2px (4.4px base unit).
- Radius: `--radius-sm` 8px, `--radius-md` 16px, `--radius-lg` 28px. Cards and the contact panel round further to `radius-lg * 1.15`; buttons, tags, and inputs go full pill (`999px`).

## Elevation

- `--shadow-sm` / `--shadow-md` / `--shadow-lg` — soft ink-tinted shadows (`color-mix` against `#2e2b25`), no hard black shadows.

## Component Patterns

### Buttons
- `.btn-primary` — solid accent fill, cream text. Primary CTA only (Email me, resume actions).
- `.btn-secondary` — outlined with divider color.
- `.btn-ghost` — text-only accent, used for "view all" style links.

### Cards
- `.card` — surface background, `radius-lg * 1.15`, no border. Elevation via `.elev-sm`/`.elev-md`/`.elev-lg`, not borders.
- Project cards lift on hover (`translateY(-4px)` + `shadow-lg`).

### Tags
- Pill-shaped, 11px, no border by default. `.tag-neutral` / `.tag-accent-2` for filled variants, `.tag-outline` for outlined (used on project cards).

### Stats
- Circular (`aspect-ratio: 1/1`, `border-radius: 999px`) tiles alternating accent/accent-2 tints — not cards.

### Navigation
- Sticky top nav, translucent cream background with `backdrop-filter: blur(6px)`. No border; separation comes from the blur + slight opacity shift on scroll.

## Motion

- `revealUp`, `heroFade` on section/hero entrance; `glowPulse` and `floatSlow` on decorative background blobs.
- All animation disabled under `prefers-reduced-motion: reduce`; `html { scroll-behavior: smooth }` for anchor nav, also disabled under reduced motion.

## Accessibility

- Text/background contrast: `#201e1d` on `#f5ead8` exceeds WCAG AAA.
- `:focus-visible` gets a 2px accent outline; default `:focus` is suppressed only where a visible alternative exists.
- Semantic landmarks: `<nav>`, `<section id="...">` per content block, heading hierarchy h1 → h2 → h3.

## Responsive

- Single breakpoint at 800px: hero grid, stats grid, stack education/certifications columns, and the contact panel all collapse to one column; hero photo shrinks to 160px.

## Font Fallback Chain

```
Headings: Caprasimo, system-ui, sans-serif
Body:     Figtree, system-ui, sans-serif
```

---

**Version**: 2.0
**Last Updated**: July 24, 2026
**Theme**: Organic (imported from Claude Design — "Arjun Kulshreshtha Landing")
