# Aesthetic Direction: Dials + Named Philosophies

Two complementary tools. **Named philosophies** give a concrete starting
point when the user names a vibe or you need to commit to one. **The three
dials** let you quantify an arbitrary brief and keep every layout/motion/
density decision consistent with that one choice, even when no named
philosophy fits cleanly.

## Dial Inference

| Signal in the brief | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| "minimalist / clean / calm / editorial / Linear-style" | 5–6 | 3–4 | 2–3 |
| "premium consumer / Apple-y / luxury / brand" | 7–8 | 5–7 | 3–4 |
| "playful / wild / Dribbble / Awwwards / experimental / agency" | 9–10 | 8–10 | 3–4 |
| "landing page / portfolio / marketing site" (default, unqualified) | 7–9 | 6–8 | 3–5 |
| "trust-first / public-sector / regulated / accessibility-critical" | 3–4 | 2–3 | 4–5 |
| "dashboard / admin / data-dense product UI" | 2–4 | 2–3 | 7–9 |

## Use-Case Presets

| Use case | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing (SaaS, mainstream) | 7 | 6 | 4 |
| Landing (agency / creative) | 9 | 8 | 3 |
| Landing (premium consumer) | 7 | 6 | 3 |
| Portfolio (designer / studio) | 8 | 7 | 3 |
| Portfolio (developer) | 6 | 5 | 4 |
| Editorial / blog | 6 | 4 | 3 |
| Public-sector service | 3 | 2 | 5 |
| Dashboard / admin | 3 | 2 | 8 |

### What each dial band means concretely

**DESIGN_VARIANCE**
- 1–3 (Predictable): symmetrical grid, equal fr-units, centered alignment.
- 4–7 (Offset): negative-margin overlaps, varied image aspect ratios, left-aligned headers over centered data.
- 8–10 (Asymmetric): masonry, fractional-unit grids (`2fr 1fr 1fr`), large intentional empty zones.
- Mobile override: any layout above `md:` at variance 4+ collapses to strict single-column below 768px — no exceptions.

**MOTION_INTENSITY**
- 1–3 (Static): CSS `:hover`/`:active` only, no automatic animation.
- 4–7 (Fluid): `transition` with cubic-bezier easing, `animation-delay` cascades for load-ins, transform/opacity only.
- 8–10 (Advanced): scroll-triggered reveals, parallax, scroll-driven animation. See [motion.md](motion.md) for the library-specific patterns — never hand-roll `window.addEventListener('scroll', ...)` at this tier.

**VISUAL_DENSITY**
- 1–3 (Art gallery): huge section gaps (`py-32`–`py-48`), maximal whitespace.
- 4–7 (Daily app): standard spacing (`py-16`–`py-24`).
- 8–10 (Cockpit): tight paddings, no card boxes — 1px dividers separate data, numbers in `font-mono`.

## Named Aesthetic Philosophies

Use when the user names one, or when you need a concrete starting point
that a dial triple alone doesn't fully specify. Each defines typography,
color, layout, spacing, motion, and detail treatment together — pick one,
don't mix two in the same surface.

### Dieter Rams (Functionalist)
Less but better. Every element earns its place.
- **Type**: clean sans (Helvetica Neue, Suisse Intl, Akkurat). Tight heading letterspacing, generous body line-height. One strict size scale.
- **Color**: monochromatic + single functional accent. Color is information, not decoration.
- **Layout**: strict grid, no asymmetry for its own sake.
- **Motion**: minimal — state changes and reveals only.
- **Details**: subtle borders/dividers over shadows; sparing, consistent radii.

### Swiss / International Typographic
Objectivity through structure. The grid is sacred.
- **Type**: strong sans (Neue Haas Grotesk, Univers, Aktiv Grotesk). Dramatic heading/body scale contrast. All-caps subheads with wide tracking.
- **Color**: high contrast — black, white, one primary. Bold color blocks as composition.
- **Layout**: rigid multi-column grid, asymmetric balance, non-negotiable alignment.
- **Motion**: grid-respecting page transitions and scroll reveals; no bounce.
- **Details**: rules as structural elements. No gradients, no shadows.

### Japanese Minimalism (Ma)
Negative space is content. Restraint communicates sophistication.
- **Type**: thin-weight sans or elegant serif (Noto Sans, Cormorant). Line-height 1.8–2.0, small body size, large margins.
- **Color**: muted naturals (warm grey, stone, sage). Near-monochrome, subtle tonal shifts.
- **Layout**: asymmetric but balanced, off-center, large intentional empty areas.
- **Motion**: slow gentle fades (400–600ms), opacity over position, no overshoot.
- **Details**: hairline borders, subtle texture (paper grain), no hard shadows.

### Brutalist / Raw
Structure is visible. No polish is the aesthetic.
- **Type**: system/monospace (JetBrains Mono, IBM Plex Mono) or aggressive display faces.
- **Color**: black/white primary; if color, raw and clashing (construction yellow, hazard orange).
- **Layout**: visible borders, exposed box model, stacked blocks, deliberate roughness.
- **Motion**: none, or jarring instant cuts — no easing.
- **Details**: visible outlines, default form elements as intentional choice.

### Scandinavian
Warmth plus restraint. Accessible by default.
- **Type**: rounded friendly sans (Nunito, Poppins, Circular).
- **Color**: warm whites, soft blues, muted greens, clay pastels. No pure black — use charcoal.
- **Layout**: clean, open, card-based, 8–12px radii, generous but not extreme spacing.
- **Motion**: gentle natural easing, subtle hover lifts.
- **Details**: soft large-blur low-opacity shadows.

### Art Deco / Geometric
Bold symmetry. Decorative precision, statement and luxury.
- **Type**: geometric display (Futura, Poiret One, Josefin Sans), all-caps headlines with extreme tracking, serif body for contrast.
- **Color**: gold/champagne, emerald, navy, burgundy, black; metallic accents.
- **Layout**: symmetrical, centered, strong vertical axis, decorative frames.
- **Motion**: elegant staggered reveals, parallax depth.
- **Details**: geometric patterns (chevrons, sunbursts), ornamental borders.

### Neo-Memphis
Playful chaos. Anti-corporate.
- **Type**: clashing weights/styles intentionally, oversized headlines, angled text.
- **Color**: bold primaries and neons, intentional clashes, flat color (no gradients).
- **Layout**: broken grid, overlapping shapes as compositional elements.
- **Motion**: bouncy, exaggerated hover, wiggle/rotate/pop.
- **Details**: thick borders, hard-edged bright drop shadows.

### Editorial / Magazine
Content-led. Typography does the heavy lifting.
- **Type**: display serif headlines (Playfair Display, Fraunces, Instrument Serif — but see [anti-slop.md](anti-slop.md) on serif overuse), clean sans body, dramatic scale (72–120px heroes), pull quotes, drop caps.
- **Color**: minimal — black/white + one editorial accent.
- **Layout**: strong 3–5 column grid, full-bleed images, mixed column widths.
- **Motion**: scroll-triggered reveals, image parallax, smooth page transitions.
- **Details**: thin rule dividers, caption typography, print-inspired metadata.

## Implementation Notes That Apply to Any Philosophy

- Load distinctive fonts (Google Fonts/CDN or self-hosted). Avoid generic
  defaults for a "distinctive" brief — but see [anti-slop.md](anti-slop.md)
  for when the *safe* choice (Inter, system fonts) is actually correct
  (public-sector, accessibility-first, explicitly-requested neutral).
- Use CSS variables for color/spacing tokens — a dominant color with sharp
  accents outperforms an evenly-distributed "safe" palette.
- Match implementation complexity to the philosophy: a Dieter Rams
  interface might be 50 lines of precise CSS; a Neo-Memphis interface
  might be 300 lines of creative chaos. Both are correct for their brief.
