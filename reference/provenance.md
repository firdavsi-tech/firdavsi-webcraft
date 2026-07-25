# Provenance

Firdavsi-Webcraft was synthesized from eleven installed community/official skills,
studied in full (not just their descriptions) before writing a single line
of this skill. Kept for transparency and for future maintenance — if one
of these upstream skills ships a major revision, this is the map of what
came from where and why.

| Source | Installs | What was taken | What was left out and why |
|---|---|---|---|
| `pbakaus/impeccable@frontend-design` | 54.1K | The mode framework (Persuade/Operate/Read/Experience) and the refine-vs-redesign distinction in `SKILL.md` and `redesign.md` | Its command router (`shape`, `critique`, `audit`, `polish`, `bolder`...) and script-based tooling (`context.mjs`, hooks, doctor) — that's a whole separate product surface, not content to fold into a synthesized reference skill |
| `anthropics/skills@frontend-design` (via `julianoczkowski/designer-skills` fork, near-identical content) | 701K | All eight named aesthetic philosophies with their concrete type/color/layout/motion specs, in `philosophies.md` | Its dark-mode and mobile-first sections were folded into `SKILL.md`'s non-negotiables instead, since `design-taste-frontend` covered the same ground with more enforceable specifics |
| `leonxlnx/taste-skill@design-taste-frontend` (v2) | 286K | The three-dial system, the design-system honesty map, the entire anti-slop tell list, the pre-flight checklist, the redesign audit protocol | Trimmed hard: the source is 1200 lines with some content (the exact "Motion-Engine Bento Paradigm" archetypes, the full pattern-name vocabulary in its Section 10, GSAP sticky-stack/horizontal-pan code skeletons) cut for being either too narrow a use case or duplicative of what's already in `motion.md` |
| `leonxlnx/taste-skill@design-taste-frontend-v1` | 126K | Cross-checked against v2 to confirm which anti-slop rules were stable across both versions (worth keeping) vs. v1-only cruft (safe to drop) | Nothing taken directly — v2 is a strict superset with better-reasoned rules |
| `patricio0312rev/skills@framer-motion-animator` | 8.4K | Nearly all code examples in `motion.md`'s cookbook section (entrance, stagger, gestures, layout, reduced motion, transition presets) | Its Next.js-App-Router-specific `template.tsx` page-transition example — replaced with the router-agnostic pattern that also documents the `AnimatePresence` pitfall below |
| `dylantarre/animation-principles@framer-motion` + `@motion-designer` | 1.3K + 1.1K | The "why" framing — Disney's principles reduced to the subset that maps cleanly to UI motion (anticipation, follow-through, easing, secondary action, exaggeration, appeal) | The other six Disney principles (squash-and-stretch, staging, arc, timing, solid drawing, straight-ahead-vs-pose-to-pose) — genuinely more relevant to character animation than typical UI work, so cut to keep the section focused |
| `hairyf/skills@motion` | 1K | The progressive-disclosure architecture itself (a lean root file, deep topics in per-file references) — modeled by this skill's own `SKILL.md` → `reference/*.md` structure | Its full API reference-file index (motion values, gestures, layout, vanilla JS/Vue usage) — out of scope; this skill assumes React + `motion/react`/`framer-motion` |
| `arvindrk/extract-design-system@extract-design-system` | 126K | The entire workflow and safety-boundaries section, in `extract-tokens.md` | Nothing cut — it's a narrow, complete, well-scoped tool wrapper |
| `wshobson/agents@tailwind-design-system` | 55.9K | The Tailwind v4 CSS-first token setup, OKLCH color usage, v3→v4 migration table, in `design-systems.md` | Its deferred `references/details.md` (not read — the root file pointed to it but the file wasn't inspected as part of this synthesis) |
| `sickn33/antigravity-awesome-skills@ui-ux-designer` | 2.4K | Used only as a checklist of *topics* a complete design skill should touch (research, IA, cross-platform, governance) to sanity-check this skill's coverage | Nearly everything else — the source is a generic persona template (Capabilities / Behavioral Traits / Knowledge Base prose) with almost no enforceable rules or code, the weakest source reviewed |
| `mindrally/skills@accessibility-a11y` | 2.3K | Taken close to wholesale into `accessibility.md` — it was already correctly scoped and concrete | Nothing significant cut |

Three items from the original research list were **not installable** via
`npx skills add` and are absent from both the installed-skills set and
this synthesis: `smithery.ai@frontend-design` (not a valid git reference),
`nextlevelbuilder/ui-ux-pro-max-skill@ckm:design-system` (same), and
`heygen-com/hyperframes@tailwind` (the `hyperframes` repo has no skill
named `tailwind` — it's a video/motion-graphics skill collection, unrelated
to CSS despite the misleading name match in search results).

One piece of content in this skill exists in **none** of the source
material: the `AnimatePresence` exit-tracking troubleshooting section in
`motion.md`. It was diagnosed firsthand while shipping a motion-driven
React site earlier in the same session this skill was written — isolated
down to a bare local-state toggle to rule out routing as the cause, then
confirmed to reproduce identically across two `framer-motion` major
versions. None of the eleven source skills mention it.
