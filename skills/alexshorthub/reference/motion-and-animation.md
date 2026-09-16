# Motion and animation

## Decide whether to animate at all, before picking a library

| How often will the user see this | Decision |
|---|---|
| 100+ times a day (keyboard shortcuts, command palette toggle) | No animation, ever |
| Tens of times a day (hover states, list navigation) | Remove it or cut it drastically |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare or first-time (onboarding, empty-state reveals, celebrations) | Room for real delight |

Never animate a keyboard-initiated action: at high repetition, animation reads as latency, not polish.

**Motion must be motivated.** Before adding any animation, state in one sentence what it communicates: hierarchy (draws attention to the right thing), storytelling (reveals content in an order that matches a narrative), feedback (acknowledges a user action), or state transition (shows that something changed). "It looked cool" is not a valid answer for anything the user sees often. Reaching for GSAP or a scroll hijack because the library is available, without a one-sentence justification, is the tell of un-motivated motion.

**Claimed motion must be shown.** If the brief's motion knob (see [design-direction.md](design-direction.md#the-three-knobs)) is set above the low end, the shipped page must actually move: entry transitions on the hero, scroll-reveal on key sections, hover physics on CTAs, at minimum. A static page claiming a high motion value is broken. Conversely, if working motion can't be shipped in the available scope, lower the knob and ship a clean static page rather than half-building motion with cut-off ScrollTriggers or missing cleanup.

## Easing and duration

- Entering or exiting → `ease-out` (starts fast, feels responsive). Never `ease-in` for UI: it delays the moment the user is watching most closely, so it reads as sluggish even at an identical duration.
- Moving or morphing in place → `ease-in-out`.
- Hover/color change → standard `ease`.
- Constant motion (marquee, progress bar) → `linear`.
- Use a custom cubic-bezier, not the bare CSS keyword. Built-in easings are too weak to feel intentional. A strong out-curve: `cubic-bezier(0.23, 1, 0.32, 1)`.

| Element | Duration |
|---|---|
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers | 200-500ms |
| Marketing/explanatory animation | can run longer |

Keep UI animation under 300ms as a rule. A faster animation is perceived as a faster app even when nothing else changed.

## Component-level rules

- Buttons: `transform: scale(0.97)` on `:active`, ~160ms ease-out, for instant press feedback.
- Never animate an entrance from `scale(0)`: nothing in the physical world appears from literally nothing. Start from `scale(0.9)` to `scale(0.95)` combined with opacity.
- Popovers scale in from their trigger's origin, not the viewport center. Modals are the exception: they stay centered because they aren't anchored to a trigger.
- After the first tooltip in a group opens, subsequent tooltips in the same group open instantly (skip the delay and the transition). This makes the whole group feel faster without weakening the original delay's purpose of preventing accidental activation.
- Prefer CSS transitions over keyframe animations for anything that can be re-triggered rapidly (toasts, toggles): transitions can be interrupted and retargeted mid-flight, while keyframes restart from zero.
- If a crossfade between two states looks wrong despite correct timing, add a light `filter: blur(2px)` during the transition. It blends the two states instead of showing them as two overlapping objects.

## Additional CSS and gesture techniques

- **Gate hover effects behind `@media (hover: hover) and (pointer: fine)`.** Touch devices fire hover on tap, which turns a hover animation into an unwanted false trigger on every tap.
- **Stagger delays stay short: 30-80ms between items.** Longer delays make the interface feel slow, and a stagger is decorative: never block interaction while it's still playing.
- **Enter and exit don't share a duration.** Exit should generally be faster than enter (e.g., a 2s deliberate press paired with a 200ms snappy release): slow where the user is deciding, fast where the system is responding.
- **`clip-path` is an animation tool, not just a shape tool.** `clip-path: inset(top right bottom left)` animates cleanly and is hardware-accelerated: use it for directional reveals (`inset(0 100% 0 0)` to `inset(0 0 0 0)` for a left-to-right reveal), a hold-to-delete affordance (slow linear fill on `:active`, fast ease-out snap-back on release), scroll-triggered image reveals, and before/after comparison sliders (clip one of two overlaid images at the drag position), all without extra DOM nodes.
- **Gesture/drag physics**, for any drag-to-dismiss or swipeable surface:
  - Dismiss on velocity, not just distance: compute `distance / elapsedTime` and dismiss above roughly `0.11`, so a quick flick dismisses even if it didn't cross the full distance threshold.
  - Apply damping (not a hard stop) when a drag passes its natural boundary. The further past the boundary, the less it moves, like real physical resistance.
  - Capture the pointer once a drag starts so it keeps tracking even if the cursor leaves the element's bounds, and ignore additional touch points after the drag begins so a second finger can't hijack the position.

## Springs

Use spring physics, not fixed-duration tweens, for: drag with momentum, anything that should feel alive (a magnetic hover, a dynamic-island-style morph), gestures that can be interrupted mid-motion, and decorative mouse-tracking. Springs preserve velocity on interruption; duration-based animation restarts from zero, which is why a quick double-toggle looks broken with tweens and fine with springs. Keep bounce subtle (0.1-0.3); save higher bounce for drag-to-dismiss and explicitly playful moments.

Never drive a continuous, high-frequency value (mouse position, scroll progress, drag physics) through React/framework state. It re-renders the tree on every change and collapses on mobile. Use motion-value primitives instead (Motion.dev's `useMotionValue`/`useTransform`/`useSpring`, or GSAP's `quickTo`, below).

## Library routing

Don't reach for a library because it's familiar. Route by what the interaction actually needs, and never load two animation libraries into the same component tree (they compete for the same frames).

| Need | Tool |
|---|---|
| Component-scoped micro-interactions in React: hover, tap, drag, `whileInView` reveals, layout/FLIP transitions, spring physics | **Motion.dev** (`motion/react`, formerly Framer Motion) |
| Scroll-driven timelines, pinning, scrubbing, parallax, SVG path morphing, or anything that must run identically outside React (vanilla, Vue, Svelte, a CMS theme) | **GSAP** + ScrollTrigger, isolated in a dedicated leaf component with proper cleanup |
| A real interactive 3D object: a product configurator, an interactive hero scene, built visually rather than hand-coded in Three.js | **Spline**, exported as a React component or embedded scene |
| A single, simple transition on a static page with no animation library already loaded | Native CSS transitions, or `@starting-style` for entrance animation without JavaScript |

## Motion.dev - ready patterns

Default import: `import { motion, useReducedMotion } from "motion/react"`.

```tsx
// Fade-up entrance
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.6, ease: [0.22, 1, 0.36, 1] }}
/>

// Hover card: spring, not a fixed tween
<motion.div
  whileHover={{ y: -8, boxShadow: "0 20px 40px rgba(0,0,0,0.12)" }}
  transition={{ type: "spring", stiffness: 300, damping: 20 }}
/>

// Scroll reveal: lighter than GSAP for a plain "appear once" case
<motion.div
  initial={{ opacity: 0, y: 50 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, amount: 0.3 }}
/>
```

- Stagger list items with `staggerChildren` (0.1-0.2s) for rhythm. Parent (`variants`) and children must live in the same client component tree.
- Exit animations require `<AnimatePresence>` wrapping the conditionally-rendered element, plus a stable `key`.
- Use the `layout` prop only on elements whose visible position or size actually changes (reordering, expanding). Wrapping static content in `layout` "for safety" costs a measurement pass for nothing.
- Always wrap with `useReducedMotion()` and fall back to the end-state (no animation) when it's true.

## GSAP + ScrollTrigger - concrete syntax

Register once per bundle: `gsap.registerPlugin(ScrollTrigger)`.

**Trigger config.** `start`/`end` follow the format `"<trigger position> <viewport position>"`:

```javascript
gsap.to(".box", {
  x: 500,
  scrollTrigger: {
    trigger: ".box",
    start: "top center", // trigger's top hits viewport center
    end: "bottom center",
    toggleActions: "play reverse play reverse", // onEnter, onLeave, onEnterBack, onLeaveBack
  },
});
```

Key options: `pin` (pin the trigger while active, animate its children rather than the pinned element itself), `scrub` (`true` links progress directly to scroll; a number of seconds lets the playhead catch up smoothly, e.g. `scrub: 1`), `pinSpacing` (defaults to `true`, adds a spacer so layout doesn't collapse), `once`, `markers` (dev only, strip before shipping).

For many elements entering together, use `ScrollTrigger.batch()` instead of one ScrollTrigger per element. It coalesces callbacks within a short interval:

```javascript
ScrollTrigger.batch(".card", {
  interval: 0.1,
  batchMax: 4,
  onEnter: (batch) => gsap.to(batch, { opacity: 1, y: 0, stagger: 0.1, overwrite: true }),
  onLeaveBack: (batch) => gsap.set(batch, { opacity: 0, y: 50, overwrite: true }),
});
```

For a value updated on every `mousemove` (a magnetic follower), use `gsap.quickTo()` instead of creating a new tween per event:

```javascript
const xTo = gsap.quickTo("#follower", "x", { duration: 0.4, ease: "power3" });
const yTo = gsap.quickTo("#follower", "y", { duration: 0.4, ease: "power3" });
el.addEventListener("mousemove", (e) => {
  xTo(e.clientX);
  yTo(e.clientY);
});
```

### Canonical skeleton - sticky card stack

The most common ScrollTrigger failure is a card that reveals sequentially instead of actually pinning. The fix is always `start: "top top"`, not `"top center"` or `"top 80%"`.

```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function StickyStack({ cards }: { cards: React.ReactNode[] }) {
  const ref = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !ref.current) return;
    const ctx = gsap.context(() => {
      const cardEls = gsap.utils.toArray<HTMLElement>(".stack-card");
      cardEls.forEach((card, i) => {
        if (i === cardEls.length - 1) return;
        ScrollTrigger.create({
          trigger: card,
          start: "top top",
          endTrigger: cardEls[cardEls.length - 1],
          end: "top top",
          pin: true,
          pinSpacing: false,
        });
        gsap.to(card, {
          scale: 0.92,
          opacity: 0.55,
          ease: "none",
          scrollTrigger: {
            trigger: cardEls[i + 1],
            start: "top bottom",
            end: "top top",
            scrub: true,
          },
        });
      });
    }, ref);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <div ref={ref} className="relative">
      {cards.map((card, i) => (
        <div key={i} className="stack-card sticky top-0 min-h-[100dvh] flex items-center justify-center">
          {card}
        </div>
      ))}
    </div>
  );
}
```

### Canonical skeleton - horizontal scroll-hijack

Same fix applies: pin the wrapper with `start: "top top"`, scrub the inner track, and size `end` off the actual scroll distance so the pin releases exactly when the track finishes sliding.

```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function HorizontalPan({ children }: { children: React.ReactNode }) {
  const wrap = useRef<HTMLDivElement>(null);
  const track = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !wrap.current || !track.current) return;
    const ctx = gsap.context(() => {
      const distance = track.current!.scrollWidth - window.innerWidth;
      gsap.to(track.current, {
        x: -distance,
        ease: "none",
        scrollTrigger: {
          trigger: wrap.current,
          start: "top top",
          end: () => `+=${distance}`,
          pin: true,
          scrub: 1,
          invalidateOnRefresh: true,
        },
      });
    }, wrap);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <section ref={wrap} className="relative overflow-hidden">
      <div ref={track} className="flex h-[100dvh] items-center">
        {children}
      </div>
    </section>
  );
}
```

**Marquees are capped at one per page.** A horizontal scrolling text/logo band is a legitimate device once; a second one on the same page reads as filler. Pick the section where it actually serves the content and use a different layout family for the rest.

## Spline - real 3D scenes

Reach for Spline when the brief needs an actual interactive 3D object (a product configurator, an interactive hero centerpiece) built visually rather than hand-coded in Three.js. It's for scenes designed in Spline's editor, not for animating existing DOM elements.

```bash
npm install @splinetool/react-spline @splinetool/runtime
```

```jsx
import Spline from '@splinetool/react-spline';

// Basic embed
<Spline scene="https://prod.spline.design/SCENE-ID/scene.splinecode" />

// Respond to interaction with a named object in the scene
function onSplineMouseDown(e) {
  if (e.target.name === 'Button') {
    // handle it
  }
}

// Drive the scene from React: find an object, then read/set its transform
function onLoad(spline) {
  const obj = spline.findObjectByName('Product');
  obj.rotation.y += Math.PI / 4;
  obj.material.color.set(0xff6b6b);
}

// Trigger a state defined inside Spline itself, rather than animating the DOM
splineApp.current.emitEvent('mouseHover', 'Card');
splineApp.current.emitEventReverse('mouseHover', 'Card'); // play it back in reverse
```

For Next.js, use the SSR-aware entry point so a placeholder renders before the scene loads (`@splinetool/react-spline/next`), and lazy-load the component (`React.lazy` + `Suspense`) when the scene isn't above the fold. A Spline scene is heavy enough that loading it eagerly on a page where it's not the first thing seen costs real LCP.

## Forbidden animation implementation patterns

- **`window.addEventListener("scroll", ...)`.** Runs on every scroll frame, unbatched, jank-prone. Use Motion's `useScroll()`, GSAP's ScrollTrigger, `IntersectionObserver`, or CSS scroll-driven animations (`animation-timeline: view()`).
- **Scroll progress computed from `window.scrollY` into framework state.** Same problem, worse: it re-renders the component tree every frame.
- **`requestAnimationFrame` loops that write to React/framework state.** Use motion values instead (`useMotionValue`/`useTransform` in Motion.dev, `quickTo` in GSAP).

## Performance

- Animate `transform` (`x`, `y`, `scale`, `rotation`, `skew`) and `opacity` only. Avoid animating `width`, `height`, `top`, `left`, `margin`, `padding`: they trigger layout, not just compositing.
- **Motion.dev's shorthand `x`/`y`/`scale` props are not automatically hardware-accelerated.** They run through `requestAnimationFrame` on the main thread, which can drop frames exactly when the page is busiest (navigating, loading). Under real load (a dashboard-style page transitioning while data streams in), animate the full `transform` string instead: `animate={{ transform: "translateX(100px)" }}`. Keep the shorthand for simple, low-stakes cases where main-thread contention isn't a concern.
- CSS animations run off the main thread and stay smooth when JavaScript is busy. Prefer CSS for a predetermined animation and JS-driven motion only for something dynamic or interruptible.
- A CSS custom property set on a parent element triggers a style recalculation on every descendant that reads it. Updating `--drag-offset` on a list's container to drive many children's motion is expensive; set `transform` directly on the element that's actually moving instead.
- Apply `will-change: transform` only to elements that are actually animating, never as a blanket default. It costs memory as a standing layer promotion.
- Prefer `stagger` over many separate tweens with manual delays for the same animation; it's both fewer lines and cheaper to run.
- Kill or pause off-screen/inactive animations rather than leaving them running; clean up every `useEffect`-created tween, timeline, and ScrollTrigger on unmount.
- Call `ScrollTrigger.refresh()` only when layout actually changed (content loaded, images resolved), not on every resize. Debounce it.
- Grain/noise filters and similar full-bleed effects belong on a fixed, `pointer-events-none` layer, never on a scrolling container. Continuous repaint on scroll kills mobile frame rate.

## Accessibility

Every animation needs a `prefers-reduced-motion` alternative that still communicates the state change, not a blanket `animation: none` that silently removes feedback the interface depends on. Reduced motion means fewer and gentler animations, not zero: keep opacity and color transitions (they aid comprehension without triggering motion sickness), and remove transform-based movement and position changes. Any motion beyond the lowest end of the motion knob (see [design-direction.md](design-direction.md#the-three-knobs)) must honor `prefers-reduced-motion`, without exception. Infinite loops, parallax, scroll-hijacks, and magnetic-cursor physics all collapse to static/instant under reduced motion.
