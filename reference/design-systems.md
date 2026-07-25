# Real Design Systems vs Hand-Rolled: The Honesty Map

Do not invent CSS for things that have an official package, and do not
pretend a hand-rolled aesthetic trend is an official system. Mixing systems
in one project (Fluent + Carbon, or shadcn inside a Material 3 app) is a
failure state — one system per project.

## When to reach for a real design system

| Brief reads as… | Reach for | Why |
|---|---|---|
| Microsoft / enterprise SaaS / dashboards | `@fluentui/react-components` or `@fluentui/web-components` | Official Fluent UI, Microsoft tokens, accessibility done |
| Google-ish UI, Material-flavored product | `@material/web` + Material 3 tokens | Official, theme-able via Material Theming |
| IBM-style B2B / enterprise analytics | `@carbon/react` + `@carbon/styles` | Official Carbon, mature data-density patterns |
| Shopify app surfaces | Polaris web components / Polaris React | Required for Shopify admin UI |
| Atlassian / Jira-style product | `@atlaskit/*` + `@atlaskit/tokens` | Official Atlassian DS |
| GitHub-style devtool / community page | `@primer/css` or `@primer/react-brand` | Official Primer; Brand variant for marketing |
| Public-sector UK service | `govuk-frontend` | Legally/regulatorily expected |
| US public-sector / trust-first | `uswds` | Same |
| Fast local-business / agency MVP | Bootstrap 5.3 | Boring, fast, works |
| Modern accessible React foundation | `@radix-ui/themes` | Primitives + polished theme |
| Modern SaaS where you own the components | shadcn/ui (`npx shadcn@latest add ...`) | You own the code, easy to customize — never ship default state |
| Tailwind-based modern SaaS / AI marketing | Tailwind v4 utilities + `dark:` variant | Default for indie/small-team builds |

**Honesty rule:** if the brief matches one of these, install and use the
*official* package. Don't recreate its CSS by hand, and don't import a
system's tokens then override 90% of them.

## When the brief is an aesthetic, not a system

No single official package owns these. Build with native CSS + Tailwind +
a maintained component library, and be honest in code comments about
what's borrowed inspiration vs. official material.

| Aesthetic | Honest implementation |
|---|---|
| Glassmorphism / "frosted glass" | `backdrop-filter` + layered borders + highlight overlays. Solid-fill fallback for `prefers-reduced-transparency`. |
| Bento (Apple-style tile grids) | CSS Grid, mixed cell sizes. No library owns this. |
| Brutalism | Native CSS, monospace, raw borders. No library. |
| Editorial / magazine | Serif type, asymmetric grid, generous whitespace. No library. |
| Dark tech / hacker | Mono + accent neon, terminal motifs. No library. |
| Aurora / mesh gradients | SVG or layered radial gradients. No library. |
| Kinetic typography | Native CSS animation, scroll-driven animation, or GSAP for hijacks. No library. |
| **Apple Liquid Glass** | Apple documents this for **Apple platforms only** — there is no official `liquid-glass.css` for the web. A web approximation uses `backdrop-filter` + layered borders + highlights. Label it clearly as an approximation in comments; see the CSS skeleton below. |

### Apple Liquid Glass — honest web approximation

```css
.liquid-glass-web-approx {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  border-radius: 999px;
  border: 1px solid rgb(255 255 255 / .32);
  background:
    linear-gradient(135deg, rgb(255 255 255 / .30), rgb(255 255 255 / .08)),
    rgb(255 255 255 / .12);
  backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  -webkit-backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / .48),
    inset 0 -1px 0 rgb(255 255 255 / .12),
    0 18px 60px rgb(0 0 0 / .18);
}

@media (prefers-reduced-transparency: reduce) {
  .liquid-glass-web-approx {
    background: rgb(255 255 255 / .96);
    backdrop-filter: none;
    -webkit-backdrop-filter: none;
  }
}
```

`prefers-reduced-transparency` has uneven browser support — test it, and
always provide enough contrast even without blur.

## Install commands

```bash
# Material Web (Material 3)
npm install @material/web

# Fluent UI React (v9)
npm install @fluentui/react-components

# Fluent UI Web Components (framework-free)
npm install @fluentui/web-components @fluentui/tokens

# IBM Carbon
npm install @carbon/react @carbon/styles

# Radix Themes
npm install @radix-ui/themes

# shadcn/ui (open code, owned components)
npx shadcn@latest init
npx shadcn@latest add button card badge separator input

# Primer CSS (GitHub product/devtool UI)
npm install --save @primer/css

# Primer Brand (GitHub marketing UI)
npm install @primer/react-brand

# GOV.UK Frontend
npm install govuk-frontend

# USWDS (US Web Design System)
npm install uswds

# Atlassian Design System (Atlaskit)
yarn add @atlaskit/css-reset @atlaskit/tokens @atlaskit/button @atlaskit/badge @atlaskit/section-message @atlaskit/card

# Bootstrap 5.3
npm install bootstrap
```

## Canonical sources (read before reinventing)

- Material Web: https://material-web.dev/theming/material-theming/ · https://m3.material.io/develop/web
- Fluent UI: https://fluent2.microsoft.design/get-started/develop · https://github.com/microsoft/fluentui
- Carbon: https://carbondesignsystem.com/ · https://carbondesignsystem.com/developing/react-tutorial/overview/
- Shopify Polaris: https://shopify.dev/docs/api/app-home/web-components · https://polaris-react.shopify.com/components
- Atlassian: https://atlassian.design/get-started/develop · https://atlassian.design/tokens/design-tokens
- Primer: https://primer.style/ · https://github.com/primer/brand
- GOV.UK: https://design-system.service.gov.uk/components/button/
- USWDS: https://designsystem.digital.gov/components/button/
- Tailwind v4: https://tailwindcss.com/docs/dark-mode · https://tailwindcss.com/blog/tailwindcss-v4
- Radix Themes: https://www.radix-ui.com/themes/docs/components/theme
- shadcn/ui: https://ui.shadcn.com/docs

## Tailwind v4 token setup (when the brief is Tailwind-based, no official system)

```css
/* app.css */
@import "tailwindcss";

@theme {
  /* Semantic color tokens in OKLCH for better perceptual uniformity */
  --color-background: oklch(100% 0 0);
  --color-foreground: oklch(14.5% 0.025 264);
  --color-primary: oklch(14.5% 0.025 264);
  --color-primary-foreground: oklch(98% 0.01 264);
  --color-border: oklch(91% 0.01 264);
  --color-ring: oklch(14.5% 0.025 264);

  --radius-sm: 0.25rem;
  --radius-md: 0.375rem;
  --radius-lg: 0.5rem;

  --animate-fade-in: fade-in 0.2s ease-out;
  @keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
  }
}

@custom-variant dark (&:where(.dark, .dark *));

.dark {
  --color-background: oklch(14.5% 0.025 264);
  --color-foreground: oklch(98% 0.01 264);
  /* ...mirror every light-mode token */
}
```

Key v3→v4 migration facts: `tailwind.config.ts` → `@theme` in CSS;
`@tailwind base/components/utilities` → `@import "tailwindcss"`;
`darkMode: "class"` → `@custom-variant dark (&:where(.dark, .dark *))`.
Do NOT use the `tailwindcss` plugin in `postcss.config.js` for v4 — use
`@tailwindcss/postcss` or the Vite plugin instead.

Token hierarchy to keep in mind: **Brand tokens** (abstract, e.g. a raw hex)
→ **Semantic tokens** (purpose, e.g. `--color-primary`) → **Component
tokens** (specific, e.g. `bg-primary` on a button). Never skip straight
from brand to component.
