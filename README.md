# alexshorthub

A single Claude Code skill for building landing pages and marketing sites that don't read as AI-generated. It's a distillation, not a bundle: nine external design and animation resources were studied for their concrete, testable rules, and those rules were rewritten from scratch into one adaptive workflow that picks only the tools a given brief actually needs.

The one non-negotiable across every project: no default gradients, no eyebrow/badge clutter, no dot-and-sparkline decoration standing in for real data, no hand-rolled decorative SVG blobs, no filler copy padding out a hero. The skill's [anti-slop checklist](skills/alexshorthub/reference/anti-slop-checklist.md) makes each of those a mechanical, binary check rather than a vibe.

## Install

Copy the skill folder into your project (or your global skills directory):

```bash
cp -r skills/alexshorthub /path/to/your-project/.claude/skills/alexshorthub
```

Claude Code picks it up automatically for landing page, marketing site, portfolio, or redesign requests. See [skills/alexshorthub/SKILL.md](skills/alexshorthub/SKILL.md) for the full trigger description.

## How it works

1. **Read the brief** - infer page kind, audience, vibe, and any constraints that override aesthetic preference (accessibility, regulated industries, public sector). State a one-line design read before building.
2. **Set three knobs** - variance, motion, density - that steer every layout and animation decision downstream.
3. **Pick the foundation** - a real design system when the brief matches one, otherwise Tailwind plus a real component source, never hand-rolled from a blank slate.
4. **Pick the animation stack** - routed by what the interaction needs (Motion.dev for component-scoped React interactions, GSAP for scroll timelines and framework-agnostic work, Spline for real 3D scenes, plain CSS for a single static-page transition), never more than one library per page.
5. **Build**, applying the concrete typography, color, and layout rules in `reference/`, plus the redesign/scope guardrails when the request is a redesign or falls outside what this skill covers.
6. **Verify once, in a bounded pass** - anti-slop checklist and copy self-audit first, quality floor (contrast, states, responsive behavior, motion accessibility, copy) second, mechanical pre-ship checklist as the final scan. No open-ended polishing loop.

Full detail lives in [skills/alexshorthub/SKILL.md](skills/alexshorthub/SKILL.md) and the seven files under `skills/alexshorthub/reference/`.

## Sources

This repository contains original text, not copies of the sources below. Each source was cloned locally, read in full, and distilled into new rules and structure; none of their files are redistributed here. Full credit:

| Source | Author | What it contributed |
|---|---|---|
| [Impeccable](https://github.com/pbakaus/impeccable) | Paul Bakaus | The "craft floor" of absolute defaults-to-avoid (gradient text, eyebrow labels, hero-metric templates, sparklines-as-decoration), the four-mode framework (Persuade/Operate/Read/Experience), and the bounded-verification-pass discipline. |
| [Taste Skill](https://github.com/leonxlnx/taste-skill) | Leon Lin (Leonxlnx) | The three-knob system and its concrete CSS-level meaning, the brief-inference workflow, the reflex-palette warnings, most of the hero/section/CTA hard limits, the full "AI tells" catalog (em dash ban, fabricated specificity, hero/page-chrome tells, decorative dots and pills), the redesign protocol, the out-of-scope list, and the canonical GSAP sticky-stack/horizontal-pan code skeletons. |
| [Animation / Design Engineering](https://github.com/emilkowalski/skills) | Emil Kowalski | The animate-or-not decision framework, easing and duration tables, component-level motion rules (press feedback, popover origin, spring interruptibility), `clip-path` as an animation technique, gesture/drag physics (velocity-based dismissal, boundary damping), and the Motion.dev hardware-acceleration gotcha (shorthand `x`/`y`/`scale` vs. the full `transform` string). |
| [GSAP skills](https://github.com/greensock/gsap-skills) | GreenSock (official) | When to reach for GSAP over CSS or another library, the concrete ScrollTrigger config syntax (`start`/`end`, `pin`, `scrub`, `toggleActions`, `batch()`), and the performance rules (`quickTo` for frequently-updated values, transform-only animation, cleanup discipline). |
| [Motion.dev animations skill](https://github.com/199-biotechnologies/motion-dev-animations-skill) | 199 Biotechnologies | The pattern decision tree for component-scoped React animation (entrance/gesture/scroll/layout) and the ready-to-use copy-paste patterns (fade-up, hover-card, scroll-reveal) that Motion.dev is routed to in this skill. |
| [Spline interactive skill](https://github.com/freshtechbro/claudedesignskills) | freshtechbro | When a real 3D scene belongs in a build, and its concrete integration surface: the event system (`onSplineMouseDown`/`emitEvent`), programmatic object control, and the Next.js SSR/lazy-load pattern. |
| [Bklit UI](https://github.com/bklit/bklit-ui) | Bklit | The rule to never hand-roll an SVG chart when a themeable registry component exists, plus its composition pattern (root-first, grid-before-series), theming tokens, and animation defaults/replay behavior. |
| [Componentry](https://componentry.dev) | Componentry | The component-sourcing rule for pre-built, already-animated interactive components (magnetic UI, particle/liquid effects) - reach for it only when the brief specifically needs that kind of interaction. |
| [Manus.im](https://manus.im) | Manus | Referenced for its process discipline rather than any published skill file - Manus is known for verifying its own generated output before returning it. That verify-before-ship discipline shaped the "one bounded pass, report what you found" rule in `qa-and-verification.md`, distilled from public write-ups of how it operates rather than from source code. |

## License

MIT - see [LICENSE](LICENSE).
