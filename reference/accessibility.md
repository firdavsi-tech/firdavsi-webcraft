# Accessibility (WCAG / ARIA / Keyboard)

Design for all users regardless of visual, auditory, motor, or cognitive
ability. Semantic HTML first — reach for ARIA only where semantics run out.

## Semantic HTML

- Use `<header>`, `<main>`, `<footer>`, `<nav>`, `<article>`, `<section>`,
  `<aside>` as landmarks for screen-reader navigation.
- `<button>` for interactive elements — never a styled `<div>` or `<span>`.
- Proper heading hierarchy (h1–h6), never skipping a level.
- Labels associated with inputs via `for`/`id`; group related fields with
  `<fieldset>` + `<legend>`; placeholder text is a supplementary hint,
  never a label replacement.

## ARIA — only where semantics run out

- Prefer a native HTML element over an ARIA-patched `<div>` whenever one
  exists.
- `aria-label` for elements with no visible text label.
- `aria-describedby` for additional context; `aria-live` for dynamic
  content updates a screen reader should announce.
- `role="button"` only when a non-button element must genuinely act as
  one; `aria-expanded` for collapsible content; `aria-hidden="true"` for
  purely decorative elements; `aria-current="page"` for nav highlighting.

## Color and contrast

- Minimum 4.5:1 for normal text, 3:1 for large text (18px+) and UI
  components. Never use color as the sole means of conveying information
  — pair it with an icon, pattern, or text label.
- Test with a color-blindness simulator, not just eyeballing.

## Focus management

- Visible focus indicators on every interactive element — never remove
  `outline` without a replacement that's at least as visible.
- Logical tab order; manage focus explicitly when content changes
  dynamically (a modal opening should trap and move focus; closing it
  should return focus to the trigger).

## Keyboard navigation

- Every interactive element reachable and operable by keyboard alone, no
  keyboard traps.
- `tabindex="0"` for natural order, `tabindex="-1"` only for programmatic
  focus targets.
- `Enter` and `Space` both activate buttons; implement arrow-key
  navigation for complex composite widgets (tabs, menus, comboboxes).
- Touch targets ≥44×44px.

## Content

- Descriptive alt text on every meaningful image; `alt=""` (empty, not
  omitted) for purely decorative images.
- Captions for video, transcripts for audio.
- Descriptive link text — never "click here."
- Relative units (`rem`/`em`) for type; text must remain usable resized
  up to 200%. Avoid justified text (uneven word spacing hurts readability
  for many cognitive-accessibility needs).

## User preferences to respect

- `prefers-reduced-motion` — disable or simplify animation.
- `prefers-color-scheme` — support both light and dark.
- `prefers-contrast` and `prefers-reduced-transparency` where applicable.

## Testing

- **Automated**: Lighthouse accessibility audit, `axe-core` integrated
  into CI. Fix every critical/serious finding — automated tools catch
  roughly a third of real issues, so treat a clean run as a floor, not
  proof of accessibility.
- **Manual**: navigate the entire flow by keyboard only; test with a
  screen reader (VoiceOver, NVDA, or JAWS); test at 200% browser zoom;
  test with real assistive-technology users when the surface warrants it.

## CSS practices that support accessibility

- External stylesheets over inline styles (maintainability, and some
  assistive tech / user stylesheets can't override inline styles as
  cleanly).
- Flexbox/Grid for layout over legacy float hacks.
- Every `:hover` state needs a `:focus` equivalent — a mouse-only
  affordance excludes keyboard users.
