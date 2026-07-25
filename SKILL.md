---
name: firdavsi-webcraft
description: Use when the user wants to design, build, redesign, critique, audit, or polish a frontend interface, or add animation/motion to one — websites, landing pages, portfolios, dashboards, product UI, components, forms, and empty/error states. Covers aesthetic direction and named design languages, anti-generic-AI-output enforcement, choosing real vs hand-rolled design systems, Framer Motion / Motion animation (including AnimatePresence pitfalls), accessibility (WCAG/ARIA/keyboard), responsive and dark-mode implementation, and redesigns of existing sites. Also trigger for "make this look less AI-generated", "add framer motion", "this looks generic", "accessibility audit", "design system", or requests naming a design philosophy (Swiss, Brutalist, Scandinavian, minimalist, Bento, glassmorphism, etc). Not for backend-only, non-UI, or native-mobile-only work.
---

# Firdavsi-Webcraft — Frontend Design, Motion & Accessibility Craft

Synthesized from eleven community and official design/animation skills (see
[reference/provenance.md](reference/provenance.md)) plus lessons this skill's
own author hit firsthand while shipping motion-driven React sites. It exists
because no single source skill covered all three legs a real frontend task
needs: **aesthetic direction that doesn't read as generic AI output**,
**motion that's actually correct and doesn't silently hang**, and
**accessibility that isn't an afterthought**.

Core principle: **the brief wins over your taste.** A user who names a
system, a font, or an era gets that system, font, or era — even when it
conflicts with the anti-slop guidance below. This skill's rules are a
default to reach past AI clichés, not a house style to impose.

## Workflow

1. **Read the room before writing code.** State a one-line design read:
   *"Reading this as: \<page kind> for \<audience>, with a \<vibe>
   language, leaning toward \<system/aesthetic>."* If genuinely ambiguous,
   ask **one** clarifying question — never a multi-question dump. If you
   can infer confidently, don't ask.
2. **Pick the mode.** What does success look like for *this surface*, not
   the product as a whole?
   - **Persuade** — visitor decides and acts (landing, marketing, pricing). Design is the product.
   - **Operate** — visitor completes a task (app UI, dashboards, settings). Scanability and native expectations outrank expression.
   - **Read** — visitor understands something (docs, articles, changelogs). Structure for comprehension first.
   - **Experience** — visitor is inside the work (portfolios, galleries). Let the artifact lead.
3. **Explore the existing codebase first** (for any non-greenfield work): component directories, CSS/theme tokens, Tailwind config, UI framework theme, font loading, package.json UI deps. Extend/compose existing components — don't duplicate them.
4. **Choose direction, then load exactly the reference(s) that apply** — don't load all of them for a small task:

   | Need | Load |
   |---|---|
   | Naming an aesthetic, picking typography/color/layout for a vibe | [reference/philosophies.md](reference/philosophies.md) |
   | Deciding real design system (Fluent/Carbon/shadcn/GOV.UK/...) vs hand-rolled | [reference/design-systems.md](reference/design-systems.md) |
   | Avoiding generic-AI-output tells before shipping | [reference/anti-slop.md](reference/anti-slop.md) |
   | Framer Motion / Motion animation, including AnimatePresence debugging | [reference/motion.md](reference/motion.md) |
   | WCAG / ARIA / keyboard / screen-reader work | [reference/accessibility.md](reference/accessibility.md) |
   | Modernizing or reworking an existing site rather than greenfield | [reference/redesign.md](reference/redesign.md) |
   | Reverse-engineering an existing live site's tokens | [reference/extract-tokens.md](reference/extract-tokens.md) |

5. **Refinement preserves; redesign replaces.** Refinement keeps the
   incumbent identity, copy, and everything outside scope — ask before
   replacing factual copy. Redesign keeps product truth and content but
   treats the old visual as evidence, not a floor to stay above. Never
   split the difference into "polish on a discarded look." See
   [reference/redesign.md](reference/redesign.md) for the full protocol.
6. **Run the pre-flight check** in [reference/anti-slop.md](reference/anti-slop.md)
   before calling any UI work done. It is mechanical, not aspirational —
   an unticked box means the work isn't finished.

## The Three Dials

Borrowed from the highest-signal source in this synthesis (`design-taste-frontend`,
286K installs). Use these to make an arbitrary vibe request quantifiable, and
to keep layout/motion/density decisions consistent across a whole surface.

- **`DESIGN_VARIANCE`** (1–10): 1 = perfect symmetry, 10 = artsy chaos.
- **`MOTION_INTENSITY`** (1–10): 1 = static, 10 = cinematic/physics.
- **`VISUAL_DENSITY`** (1–10): 1 = art-gallery airy, 10 = cockpit/packed.

Baseline `7/6/4` for a generic landing page. Full inference table (which
vibe words map to which values, plus use-case presets) is in
[reference/philosophies.md](reference/philosophies.md) alongside the named
aesthetic vocabulary the dials pair with.

## Non-Negotiables (apply regardless of which reference you load)

- **Mobile-first.** Build the single-column 375px layout first, then scale
  up with `min-width` media queries. Touch targets ≥44×44px. Body text
  ≥16px on mobile (prevents iOS zoom-on-focus).
- **`min-h-[100dvh]`, never `h-screen`**, for full-height sections — avoids
  layout jump from the iOS Safari address bar.
- **Dark mode is default-in-scope** for any consumer-facing surface, not an
  afterthought. Use `prefers-color-scheme` plus a manual override; never
  invert colors naively; keep WCAG AA contrast in both modes; no pure
  `#000000` / `#ffffff`.
- **`prefers-reduced-motion` is mandatory** for any motion above trivial
  hover states. See [reference/motion.md](reference/motion.md) for the
  exact pattern per animation library.
- **Never animate `top`/`left`/`width`/`height`.** Only `transform` and
  `opacity` are GPU-accelerated; everything else causes layout thrash.
- **Accessibility is not optional polish.** Semantic HTML before ARIA,
  keyboard parity for every interactive element, WCAG AA contrast
  (4.5:1 normal text, 3:1 large text / UI components). Full checklist in
  [reference/accessibility.md](reference/accessibility.md).
