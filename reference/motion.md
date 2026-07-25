# Motion: Framer Motion / Motion Implementation

Combines the "why" (animation principles) with the "how" (working code)
and a troubleshooting section none of this skill's sources had — the
`AnimatePresence` router-transition hang, diagnosed firsthand.

## The Why: Animation Principles That Actually Communicate

Before reaching for a spring config, ask what the motion communicates.
Valid reasons: hierarchy (drawing attention to the right thing),
storytelling (revealing content in a sequence that matches a narrative),
feedback (acknowledging a user action), state transition (showing
something changed). "It looked cool" is not a reason — if you can't
state the reason in one sentence, drop the animation.

Disney's principles that map cleanly onto UI motion:

- **Anticipation** — a small wind-up before the real action (a button
  recoils slightly before a nav transition) makes the action feel
  intentional rather than instant/robotic.
- **Follow-through / overlapping action** — nothing stops at once; stagger
  child elements so faster ones lead and heavier ones lag slightly.
- **Slow in / slow out (easing)** — ease into and out of motion; sharp
  curves read as snappy, gentle curves read as graceful. Springs are
  usually more natural than linear tweens for UI.
- **Secondary action** — a supporting movement that reinforces the
  primary one without distracting from it (a card's shadow "breathes" as
  it opens).
- **Exaggeration** — subtle for UI (button scales to 102–105% on hover,
  not 150%); match the exaggeration to the brand's energy level.
- **Appeal** — motion should be captivating, not just "pretty." If the
  viewer's eye keeps moving past it without noticing, it wasn't worth
  animating.

## The How: Framer Motion / Motion Cookbook

Package is `framer-motion` (legacy import path still works) or the
current `motion/react` — prefer `motion/react` in new code, the API is
identical.

### Entrance and hover

```tsx
import { motion } from 'framer-motion'

export function FadeIn({ children }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5 }}
    >
      {children}
    </motion.div>
  )
}

export function ScaleOnHover({ children }) {
  return (
    <motion.div
      whileHover={{ scale: 1.05 }}
      whileTap={{ scale: 0.95 }}
      transition={{ type: 'spring', stiffness: 400, damping: 17 }}
    >
      {children}
    </motion.div>
  )
}
```

### Staggered lists

```tsx
const containerVariants = {
  hidden: { opacity: 0 },
  visible: { opacity: 1, transition: { staggerChildren: 0.1, delayChildren: 0.2 } },
}
const itemVariants = {
  hidden: { opacity: 0, y: 20 },
  visible: { opacity: 1, y: 0, transition: { type: 'spring', stiffness: 300, damping: 24 } },
}

export function StaggeredList({ items }) {
  return (
    <motion.ul variants={containerVariants} initial="hidden" animate="visible">
      {items.map((item, i) => <motion.li key={i} variants={itemVariants}>{item}</motion.li>)}
    </motion.ul>
  )
}
```

For grids larger than ~20 items, cap `staggerChildren` well below the
default 0.06–0.1s (try `Math.min(0.04, 1.5 / items.length)`) or the tail
items visibly lag behind the scroll position that triggered them.

### Scroll-triggered reveal (lightweight, no pinning)

```tsx
import { motion } from 'framer-motion'

export function RevealOnScroll({ children }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 24 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, margin: '-10% 0px' }}
      transition={{ duration: 0.6, ease: 'easeOut' }}
    >
      {children}
    </motion.div>
  )
}
```

`whileInView` uses IntersectionObserver under the hood — it does **not**
depend on animation-frame compositing the way exit animations do (see
Troubleshooting below), so it's reliable even in constrained/headless
render contexts. Prefer it over `window.addEventListener('scroll', ...)`,
which is banned outright: it re-renders on every frame and is jank-prone.
For actual scroll-linked values (parallax, progress bars), use
`useScroll` + `useTransform`, never raw `scrollY` in React state.

### Gestures: drag and swipe-to-dismiss

```tsx
export function DraggableCard() {
  return (
    <motion.div
      drag
      dragConstraints={{ left: -100, right: 100, top: -100, bottom: 100 }}
      dragElastic={0.2}
      whileDrag={{ scale: 1.1, cursor: 'grabbing' }}
    />
  )
}
```

### Shared-element / layout transitions

```tsx
import { motion, LayoutGroup } from 'framer-motion'

export function Tabs({ tabs, activeTab, onTabChange }) {
  return (
    <LayoutGroup>
      <div className="flex gap-2">
        {tabs.map((tab) => (
          <button key={tab.id} onClick={() => onTabChange(tab.id)} className="relative px-4 py-2">
            {activeTab === tab.id && (
              <motion.div layoutId="activeTab" className="absolute inset-0 bg-blue-500 rounded-lg"
                transition={{ type: 'spring', stiffness: 500, damping: 30 }} />
            )}
            <span className="relative z-10">{tab.label}</span>
          </button>
        ))}
      </div>
    </LayoutGroup>
  )
}
```

### Reduced motion (mandatory above trivial hover)

```tsx
import { useReducedMotion } from 'framer-motion'

export function AccessibleAnimation({ children }) {
  const shouldReduceMotion = useReducedMotion()
  return (
    <motion.div
      initial={{ opacity: 0, y: shouldReduceMotion ? 0 : 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: shouldReduceMotion ? 0 : 0.5 }}
    >
      {children}
    </motion.div>
  )
}
```

### Transition presets worth reusing

```ts
export const transitions = {
  spring: { type: 'spring', stiffness: 300, damping: 24 },
  springBouncy: { type: 'spring', stiffness: 500, damping: 15 },
  smooth: { type: 'tween', duration: 0.3, ease: 'easeInOut' },
  snappy: { type: 'tween', duration: 0.15, ease: [0.25, 0.1, 0.25, 1] },
} as const
```

## Troubleshooting: `AnimatePresence` That Never Unmounts

**Symptom:** you wrap route/page content (or any conditionally-rendered
element) in `<AnimatePresence mode="wait">`, the state/route genuinely
changes (you can confirm the new value in React DevTools or via a
console log in an effect), but the DOM keeps showing the *old* content
forever. With `mode="wait"` removed, the *new* content mounts fine, but
the *old* content also never unmounts — both sit in the DOM at once.

**Root cause, confirmed by isolating it down to a bare local-state
toggle** (two `motion.div`s swapped by a boolean, zero routing involved):
`AnimatePresence`'s exit path depends on receiving an animation-complete
callback, which in turn depends on the browser actually compositing
animation frames for that tab. In any environment where the tab isn't
being visually rendered/composited (a headless or backgrounded browser
automation context is the common case — the same environment where
`element.scrollIntoView({ behavior: 'smooth' })` and `window.scrollTo({
behavior: 'smooth' })` also silently no-op), that completion callback
never fires, so the exiting element is deferred forever. This reproduced
identically across framer-motion 11.18.2 and 12.42.2, ruling out a
version-specific regression — it's an artifact of the render context, not
the library. In a normally visible browser tab this exact code works.

**Practical fix if you can't verify a real compositing browser is
available** (e.g. building something you'll test via a browser-automation
tool rather than opening it yourself): don't depend on `AnimatePresence`
exit tracking for anything correctness-critical, like route content
switching. Make the *entrance* animation the whole show:

```tsx
// Instead of relying on AnimatePresence to defer unmount of the old page:
function App() {
  const location = useLocation()
  const Page = pages[location.pathname] ?? Home
  return (
    // No AnimatePresence. React's own reconciliation unmounts the old
    // page instantly on key change; the new one plays its entrance.
    <motion.div key={location.pathname} initial={{ opacity: 0, y: 12 }} animate={{ opacity: 1, y: 0 }}>
      <Page />
    </motion.div>
  )
}
```

This sacrifices the fade-*out* crossfade but keeps the fade-*in*, and is
unconditionally correct because it never depends on an animation
completion callback — React's synchronous unmount/mount handles the
old-to-new swap regardless of whether frames are compositing.

Apply the same instinct anywhere else `AnimatePresence` gates something
users depend on actually happening: a "back to top" button that must
disappear, a modal that must unmount for a screen reader to move on. If
you can verify a real, visible browser (ask the user, or check whether a
screenshot tool actually returns pixels rather than a "not compositing"
error), `AnimatePresence` is fine and gives a nicer crossfade — just
don't assume it silently works in every render context.

**Independently:** `mode="wait"` specifically blocks the *entering*
element from mounting until the *exiting* one finishes — so this bug's
worst symptom (page seemingly frozen on the old route after a real
navigation) is caused by `mode="wait"`'s wait condition never resolving,
not by the entering component itself being broken. Dropping `mode="wait"`
(plain `<AnimatePresence>`, crossfade instead of sequential) unblocks
entry but still leaves the old element stuck if exit-completion never
fires — so it's a partial mitigation, not a fix, in a non-compositing
context.

## Performance Rules

- Animate only `transform` and `opacity` — the only GPU-accelerated
  properties. Never animate `top`, `left`, `width`, `height`.
- Continuous/magnetic-hover physics: use `useMotionValue` +
  `useTransform`, never `useState` — `useState` re-renders the React tree
  every frame and collapses on mobile.
- Isolate any perpetually-looping animation (pulse, shimmer, marquee) in
  its own small, memoized client component so it doesn't force re-renders
  in a parent layout.
- `staggerChildren` requires the parent (`variants`) and children in the
  *same* client component tree — if data is fetched async, pass it as
  props into a centralized parent motion wrapper rather than fetching
  inside the staggered children.
- Never mix GSAP/Three.js with Motion in the same component tree — they
  fight over the same animation frame. Use Motion for UI/state-change
  motion; reach for GSAP+ScrollTrigger only for full-page scrolltelling
  or scroll-hijacking, isolated in its own leaf component with a strict
  `useEffect` cleanup (`gsap.context(...).revert()` on unmount).
