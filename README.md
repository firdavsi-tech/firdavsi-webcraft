# firdavsi-webcraft

A [Claude Code](https://claude.com/claude-code) skill for frontend design, motion, and accessibility — aesthetic direction that doesn't read as generic AI output, motion that's actually correct, and accessibility that isn't an afterthought.

## Why this exists

No single existing skill covered all three legs a real frontend task needs. `firdavsi-webcraft` was synthesized from eleven community and official design/animation skills, each read in full and evaluated for what to keep, what to cut, and why (see [reference/provenance.md](reference/provenance.md) for the complete breakdown). It also documents one bug found nowhere else in the source material: a `Framer Motion` `AnimatePresence` exit-tracking failure mode, diagnosed and written up firsthand.

## What it covers

- **Aesthetic direction** — eight named design philosophies (Dieter Rams, Swiss, Japanese Minimalism, Brutalist, Scandinavian, Art Deco, Neo-Memphis, Editorial), plus a three-dial system (`DESIGN_VARIANCE` / `MOTION_INTENSITY` / `VISUAL_DENSITY`) for quantifying an arbitrary vibe request
- **Anti-slop enforcement** — a mechanical pre-flight checklist against generic-AI-output tells: em-dash bans, eyebrow-label restraint, serif discipline, premium-consumer palette bans, hero-viewport rules, and more
- **Real vs. hand-rolled design systems** — an honesty map for when to reach for Fluent UI, Carbon, GOV.UK Frontend, shadcn/ui, or Tailwind utilities instead of inventing CSS
- **Framer Motion / Motion** — a working code cookbook (entrance, stagger, gestures, scroll-linked values, reduced motion) plus a documented `AnimatePresence` pitfall and its fix
- **Accessibility** — a concrete WCAG / ARIA / keyboard-navigation checklist
- **Redesign protocol** — greenfield vs. refine vs. overhaul, an audit-first workflow, and what should never change silently

## Structure

```
firdavsi-webcraft/
  SKILL.md                       Router: workflow, the three dials, non-negotiables
  reference/
    philosophies.md              Named aesthetic languages + dial inference tables
    design-systems.md            Real design system vs. hand-rolled honesty map
    anti-slop.md                 Generic-AI-output tells + pre-flight checklist
    motion.md                    Framer Motion cookbook + AnimatePresence pitfall
    accessibility.md             WCAG / ARIA / keyboard checklist
    redesign.md                  Greenfield vs. refine vs. overhaul protocol
    extract-tokens.md            Reverse-engineering tokens from a live site
    provenance.md                Full source-by-source breakdown of what was kept and cut
```

`SKILL.md` stays a lean router; each reference file is loaded only when the task actually needs it, rather than dumping the whole skill into context at once.

## Installing

Copy this repository into your project's or your global `.claude/skills/` directory:

```bash
git clone https://github.com/firdavsi-tech/firdavsi-webcraft.git .claude/skills/firdavsi-webcraft
```

Or install via the [skills CLI](https://skills.sh/):

```bash
npx skills add firdavsi-tech/firdavsi-webcraft
```

## Companion skill

Pairs with [firdavsi-shipcraft](https://github.com/firdavsi-tech/firdavsi-shipcraft) — where this skill decides what an interface looks and feels like, `firdavsi-shipcraft` covers making sure it actually works: performance, SEO, responsive behavior, design tokens, and component documentation.
