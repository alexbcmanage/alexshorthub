# Motion and animation

## Decide whether to animate at all, before picking a library

| How often will the user see this | Decision |
|---|---|
| 100+ times a day (keyboard shortcuts, command palette toggle) | No animation, ever |
| Tens of times a day (hover states, list navigation) | Remove it or cut it drastically |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare or first-time (onboarding, empty-state reveals, celebrations) | Room for real delight |

Never animate a keyboard-initiated action — at high repetition, animation reads as latency, not polish.

Every animation needs a purpose beyond "it looks good": spatial consistency (a toast that enters and exits from the same edge), state indication, explaining how something works, confirming a press, or preventing a jarring instant appear/disappear. If the only answer is "it looks cool" and the user will see it often, skip it.

## Easing and duration

- Entering or exiting → `ease-out` (starts fast, feels responsive). Never `ease-in` for UI — it delays the moment the user is watching most closely, so it reads as sluggish even at an identical duration.
- Moving or morphing in place → `ease-in-out`.
- Hover/color change → standard `ease`.
- Constant motion (marquee, progress bar) → `linear`.
- Use a custom cubic-bezier, not the bare CSS keyword — built-in easings are too weak to feel intentional. A strong out-curve: `cubic-bezier(0.23, 1, 0.32, 1)`.

| Element | Duration |
|---|---|
| Button press feedback | 100–160ms |
| Tooltips, small popovers | 125–200ms |
| Dropdowns, selects | 150–250ms |
| Modals, drawers | 200–500ms |
| Marketing/explanatory animation | can run longer |

Keep UI animation under 300ms as a rule — a faster animation is perceived as a faster app even when nothing else changed.

## Component-level rules

- Buttons: `transform: scale(0.97)` on `:active`, ~160ms ease-out, for instant press feedback.
- Never animate an entrance from `scale(0)` — nothing in the physical world appears from literally nothing. Start from `scale(0.9)`–`scale(0.95)` combined with opacity.
- Popovers scale in from their trigger's origin, not the viewport center. Modals are the exception — they stay centered because they aren't anchored to a trigger.
- After the first tooltip in a group opens, subsequent tooltips in the same group open instantly (skip the delay and the transition) — this makes the whole group feel faster without weakening the original delay's purpose of preventing accidental activation.
- Prefer CSS transitions over keyframe animations for anything that can be re-triggered rapidly (toasts, toggles) — transitions can be interrupted and retargeted mid-flight; keyframes restart from zero.
- If a crossfade between two states looks wrong despite correct timing, add a light `filter: blur(2px)` during the transition — it blends the two states instead of showing them as two overlapping objects.

## Springs

Use spring physics, not fixed-duration tweens, for: drag with momentum, anything that should feel alive (a magnetic hover, a dynamic-island-style morph), gestures that can be interrupted mid-motion, and decorative mouse-tracking. Springs preserve velocity on interruption; duration-based animation restarts from zero, which is why a quick double-toggle looks broken with tweens and fine with springs. Keep bounce subtle (0.1–0.3); save higher bounce for drag-to-dismiss and explicitly playful moments.

## Library routing

Don't reach for a library because it's familiar — route by what the interaction actually needs, and never load two animation libraries into the same page.

| Need | Tool |
|---|---|
| Component-scoped micro-interactions in React: hover, tap, drag, `whileInView` reveals, layout/FLIP transitions, spring physics | **Motion.dev** (`motion/react`, formerly Framer Motion) |
| Scroll-driven timelines, pinning, scrubbing, parallax, SVG path morphing, or anything that must run identically outside React (vanilla, Vue, Svelte, a CMS theme) | **GSAP** + ScrollTrigger |
| A real interactive 3D object — a product configurator, an interactive hero scene — built visually rather than hand-coded in Three.js | **Spline**, exported as a React component or embedded scene |
| A single, simple transition on a static page with no animation library already loaded | Native CSS transitions, or `@starting-style` for entrance animation without JavaScript |

Motion.dev and GSAP overlap on scroll reveals; the deciding factor is whether the project already has a component framework doing the state management (favor Motion.dev) or needs a framework-agnostic timeline that also touches SVG/Canvas (favor GSAP). Spline is for scenes designed visually, not for animating existing DOM elements — don't reach for it to animate a button.

## Accessibility

Every animation needs a `prefers-reduced-motion` alternative that still communicates the state change — not a blanket `animation: none` that silently removes feedback the interface depends on. A reduced-motion fallback should swap the animated transition for an instant one, not delete the state indication entirely.
