# Anti-Slop: Generic-AI-Output Tells and the Pre-Flight Check

This is the single most differentiated content in this skill's source
material (from `design-taste-frontend`, validated against real production
tests). None of it fires automatically — it's a checklist to run before
calling UI work finished, and an override always exists when the brief
explicitly asks for the "banned" thing.

## Typography

- **Avoid Inter as the unexamined default.** Reach for `Geist`, `Outfit`,
  `Cabinet Grotesk`, `Satoshi`, or a brand-appropriate serif first.
  **Override:** Inter is correct for a neutral/standard/Linear-style brief,
  or public-sector/accessibility-first sites.
- **Serif is discouraged as a default**, not banned. "It feels creative /
  premium" is not a reason. Use serif only when the brief literally names
  one, or the aesthetic is genuinely editorial/luxury/publication/heritage
  and you can articulate why *this* serif fits *this* brand. Specifically
  avoid `Fraunces` and `Instrument Serif` as defaults — they're the two
  most-reused LLM display serifs. Never mix a serif word into a sans
  headline for "visual interest" — use italic/bold of the *same* family.
- **No oversized H1s that just scream.** Control hierarchy with weight and
  color, not raw scale.
- **Italic + descender clearance:** any italic word containing `y g j p q`
  needs `leading-[1.1]` minimum plus a `pb-1`/`mb-1` reserve, or the
  descender clips.

## Color

- **Max one accent color**, saturation under 80% by default. Neutral bases
  (Zinc/Slate/Stone) with one high-contrast accent beats an evenly
  saturated palette.
- **The "AI purple" tell**: no default purple/blue button glows or neon
  gradients. **Override:** fine if the brand/brief explicitly asks for
  violet — execute with intent (consistent palette, restrained gradient).
- **Premium-consumer palette ban:** for cookware/wellness/artisan/luxury
  DTC briefs, the reflexive default is warm beige/cream + brass/clay/
  oxblood + espresso near-black text. It's overused to the point of
  erasing brand identity. Rotate instead: cold-luxury silver/chrome/smoke,
  forest deep-green/bone/amber, black-and-tan sharp contrast, cobalt +
  cream, terracotta + slate, olive + brick + paper, or pure monochrome +
  one saturated pop. Don't reuse the same family twice in a row.
  **Override:** the beige+brass family is fine when the brand brief names
  it explicitly.
- **One palette, locked.** Once an accent is chosen it's used identically
  across every section — no warm-grey site suddenly getting a blue CTA in
  section 7.

## Layout

- **No centered-hero default above `DESIGN_VARIANCE` 4.** Prefer split
  screen, left/right asymmetry, or scroll-pinned structures.
  **Override:** centered is correct for editorial/manifesto/launch briefs
  where the message *is* the design.
- **No 3-equal-column feature cards.** The "three identical cards
  horizontally" row is the most reused AI layout. Use 2-column zig-zag,
  asymmetric grid, or horizontal scroll instead.
- **One corner-radius system per page** (all-sharp, all-soft, or a
  documented mixed rule like "buttons pill, cards 16px, inputs 8px") —
  applied everywhere, not per-component whim.
- **Zigzag alternation cap:** max 2 consecutive image+text-split sections.
  A 3rd in a row is a fail — break it with a full-width, vertical-stack,
  bento, or marquee section.
- **Section-layout repetition ban:** a layout family (3-col cards,
  full-width quote, split text/image) appears at most once per page. An
  8-section page needs at least 4 different layout families.
- **Eyebrow restraint (the most-violated rule in production tests):** the
  small uppercase label above a section headline. Max **1 eyebrow per 3
  sections** (hero counts as 1). Mechanical check: count `uppercase
  tracking`-style labels across all sections; if count > ceil(sections/3),
  it fails. Usually the fix is simply dropping the eyebrow — the headline
  alone is enough.
- **Split-header ban:** "left big headline + right small explainer
  paragraph" as a section header is banned by default. Stack vertically
  (headline, then body, `max-w-[65ch]`) unless the right column carries a
  real visual/interactive element.
- **Bento grids need exact cell count** (N items → N cells, no empty
  filler cell) and real visual variation in 2–3 cells (image, gradient,
  pattern) — not six identical white-on-white text cards.

## Hero discipline (hard rules)

- Headline ≤2 lines desktop, subtext ≤20 words AND ≤4 lines, CTA visible
  without scrolling. If copy doesn't fit: cut copy or reduce font scale —
  never let the hero overflow the viewport.
- Plan font size and asset size together. Default `text-4xl md:text-5xl
  lg:text-6xl`; only go to `text-6xl md:text-7xl` for a 3–5 word headline.
  A 4-line hero headline is a font-size error, not a copy-length one.
- Hero top padding max `pt-24` at desktop — more and the content floats
  halfway down the viewport, reading as a bug.
- **Max 4 text elements in the hero**: (eyebrow OR brand strip, pick zero
  or one) + headline + subtext + CTAs (1 primary + max 1 secondary).
  Banned in the hero: tiny tagline below CTAs, trust micro-strip, pricing
  teaser, feature bullets, social-proof avatar row — all of those belong
  in a dedicated section directly below.
- "Trusted by" logo walls live under the hero, never inside it, and use
  real SVG logos (Simple Icons CDN, devicon) or a generated monogram for
  invented brands — never plain-text wordmarks. Logo only, no category
  label underneath ("Vercel" + "hosting" is noise).

## Buttons & forms (accessibility-adjacent)

- **CTA contrast:** every button's text must be readable against its
  background — WCAG AA 4.5:1 (3:1 for 18px+ text). White-on-white,
  transparent-over-photo without a scrim, `bg-white` + `text-white` are
  all shipping-blockers, not style choices.
- **CTA wrap ban:** button text must fit one line at desktop. If it wraps,
  shorten the label (3 words max for primary CTAs) — don't constrain
  button width to force a wrap.
- **No duplicate CTA intent:** "Get in touch" + "Contact us" + "Let's
  talk" on the same page is one intent said three ways. Pick one label,
  use it everywhere (nav, hero, footer).
- **Form contrast:** inputs, placeholders, focus rings, helper/error text
  all pass WCAG AA against the section background.
- Label above input, helper text present in markup, error text below
  input. Never placeholder-as-label.

## Content

- **No generic names/avatars/numbers.** "John Doe", default egg-avatar
  icons, and too-perfect numbers (`99.99%`, `1234567`) all read as
  unfinished. Use realistic messy data (`47.2%`, `+1 (312) 847-1928`) and
  invented-but-plausible names.
- **No startup-slop brand names** ("Acme", "Nexus", "SmartFlow") and no
  filler-verb copy ("Elevate", "Seamless", "Unleash", "Next-Gen").
- **Copy self-audit before shipping:** re-read every visible string —
  headlines, buttons, captions, alt text, errors. Flag anything
  grammatically broken, with an unclear referent, or that reads like an
  LLM straining to sound thoughtful (forced metaphors, mock-poetic
  micro-labels). Replace with plain functional copy.
- **Quotes ≤3 lines** of body, real attribution (name + role, never name
  alone), typographic quote marks.
- **The em-dash (`—`) is completely banned**, in headlines, labels, body
  copy, captions, and attribution — no "sparing use" exception. It's the
  single most-flagged tell in production tests. Use a period, comma, or
  regular hyphen instead. En-dash-as-separator (`2018–2026`) also becomes
  a plain hyphen.
- **No section-numbering eyebrows** (`00 / INDEX`, `001 · Capabilities`),
  no version labels in a non-launch hero (`V0.6`, `BETA`), no scroll cues
  (`Scroll ↓` — if they haven't scrolled yet, they're looking at the
  hero; they know what scroll is), no locale/weather strips unless the
  brief is genuinely place-focused or globally-distributed.

## Images

- **Priority order:** an image-generation tool first (hero photography,
  product shots, textures) → real photo URLs (`picsum.photos/seed/
  {descriptive-seed}/{w}/{h}` as a placeholder, or brand-provided assets)
  → clearly-labeled `<!-- TODO: hero photo, 1600x1200 -->` placeholders
  as a last resort, with an explicit note to the user about what's needed.
- **Div-based fake screenshots are banned** — a "product preview" built
  from styled `<div>` rectangles simulating a dashboard/terminal/task
  list is the #1 visual tell. Use a real screenshot, a generated image,
  or an actual mini component preview.
- Even minimalist/text-forward briefs need 2–3 real images (hero, one
  product/lifestyle shot, one supporting image) — a pure-text page isn't
  minimalism, it's incomplete.
- Icons from a library (Phosphor, HugeIcons, Radix, Tabler) — never
  hand-rolled SVG paths, never Lucide unless explicitly requested or
  already a project dependency.

## Theme consistency

- **One theme per page.** If the page is dark, every section is dark —
  no light-mode section sandwiched mid-scroll (exception: a deliberate,
  brief-requested single theme-switch-on-scroll device).

## Pre-Flight Check

Run every box before calling UI work done. An unticked box means the work
isn't finished — this is mechanical, not aspirational.

- [ ] One-line design read stated, dial values reasoned from the brief
- [ ] Design system chosen from [design-systems.md](design-systems.md), or aesthetic honestly labeled as hand-rolled
- [ ] Zero em-dashes anywhere on the page
- [ ] One theme (light/dark/auto) for the whole page, no mid-page flips
- [ ] One accent color used identically everywhere; one corner-radius system
- [ ] Every CTA passes contrast (WCAG AA), fits one line, no duplicate intent
- [ ] Form inputs/placeholders/focus rings pass contrast
- [ ] Hero fits the viewport: ≤2-line headline, ≤20-word subtext, CTA visible without scroll, top padding ≤`pt-24`
- [ ] Hero has ≤4 text elements, no trust-strip/tagline/pricing-teaser stuffed in
- [ ] Eyebrow count ≤ ceil(sections/3)
- [ ] No split-header pattern, no 3+ consecutive zigzag sections, no repeated layout family across the page
- [ ] Bento cell count matches content exactly, 2–3 cells have real visual variation
- [ ] Real images used (gen tool → picsum-seed → labeled placeholder), no div-based fake screenshots, no hand-rolled decorative SVGs
- [ ] Copy self-audit done — no broken/hallucinated strings, no filler verbs, no generic names/numbers
- [ ] Every animation justified in one sentence (hierarchy / storytelling / feedback / state change) — see [motion.md](motion.md)
- [ ] `prefers-reduced-motion` respected for anything above trivial hover
- [ ] Dark mode implemented and tested, not just light mode
- [ ] Mobile collapse explicit for every multi-column section
- [ ] `min-h-[100dvh]` used, never `h-screen`
- [ ] No AI-purple gradients, no Inter-by-default on a "distinctive" brief, no three-equal-cards row
- [ ] Accessibility checklist from [accessibility.md](accessibility.md) passed
