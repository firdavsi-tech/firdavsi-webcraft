# Redesign Protocol

Misclassifying greenfield vs. redesign is the single biggest source of bad
redesign output — solve this first, before touching any code.

## Detect the mode

- **Greenfield** — no existing site, or a full overhaul is explicitly
  approved. Use the dial baseline from [philosophies.md](philosophies.md).
- **Redesign — preserve** — modernize without breaking the brand. Audit
  first, extract brand tokens, evolve gradually.
- **Redesign — overhaul** — new visual language on top of existing
  content. Treat visuals as greenfield; preserve content and information
  architecture.

If ambiguous, ask **once**: *"Should this preserve the existing brand, or
are we starting visually from scratch?"*

**Refinement preserves; redesign replaces.** Refinement keeps the
incumbent identity, behavior, copy, and everything outside scope — ask
before replacing factual copy or adding claims. Redesign keeps product
truth, content, and constraints, but treats the old look as evidence and
anti-reference, not a floor to stay above. Never split the difference
into "polish on the look you're discarding."

## Audit before touching anything

Document the current state before proposing changes:

- **Brand tokens** — primary/accent colors, type stack, logo treatment,
  corner radii.
- **Information architecture** — page tree, primary nav, key conversion
  paths.
- **Content blocks** — what exists, what's doing work, what's filler.
- **Patterns to preserve** — signature interactions, a recognizable hero,
  the existing copy voice.
- **Patterns to retire** — AI-slop tells (see [anti-slop.md](anti-slop.md)),
  broken layouts, dead links, generic stock imagery, performance traps.
- **Current dial reading** — infer the existing site's `DESIGN_VARIANCE`/
  `MOTION_INTENSITY`/`VISUAL_DENSITY`. That's the starting point, not the
  baseline from philosophies.md.
- **SEO baseline** — current ranking pages, meta titles, structured data,
  OG cards. SEO regression is the #1 redesign risk.

## Preservation rules

- Don't change information architecture unless asked. Keep page slugs,
  anchor IDs, and primary nav labels stable for SEO and muscle memory.
- Extract brand colors before applying the anti-slop color rules — a
  brand that's already purple stays purple.
- Preserve copy voice unless a rewrite is requested. Visual modernization
  is not content rewrite.
- Honor existing accessibility wins — don't regress focus states, alt
  text, keyboard nav, or contrast that already worked.
- Respect existing analytics events — don't rename buttons, form fields,
  or section IDs that downstream tracking depends on.

## Modernization levers, in priority order

Apply in order, stop once the brief is satisfied:

1. **Typography refresh** — biggest visual lift per unit of risk.
2. **Spacing & rhythm** — increase section padding, fix vertical rhythm.
3. **Color recalibration** — desaturate, unify neutrals, keep the brand accent.
4. **Motion layer** — add dial-appropriate micro-interactions to existing components.
5. **Hero & key-section recomposition** — restructure the top of the funnel.
6. **Full block replacement** — only when the existing block is unsalvageable.

## Decision tree: targeted evolution vs. full redesign

- IA, content, and SEO are sound → **targeted evolution** (levers 1–4).
  Roughly 70% of the value at 40% of the risk.
- Visual debt is structural (broken IA, no design system, broken mobile)
  → **full redesign** with strict content preservation.
- The brand itself is changing → **greenfield**.

## Never change silently

Requires explicit user approval before touching:

- URL structure / route slugs.
- Primary nav labels.
- Form field names or order (breaks analytics + browser autofill).
- Brand logo or wordmark.
- Existing legal / consent / cookie copy.
