---
name: alexshorthub
description: Use when building or redesigning a landing page, marketing site, portfolio, or any frontend surface where visual quality and "not looking AI-generated" matter. Distills nine design/animation skill sources (Impeccable, Taste Skill, Emil Kowalski's design-eng, GSAP, Motion.dev, Spline, Bklit UI, Componentry.dev, and Manus.im's verification discipline) into one adaptive workflow: read the brief, pick a design direction, pick only the tools the brief actually needs, build, then run a mechanical anti-slop check before shipping. Not for backend-only work or non-visual tasks.
license: MIT
---

# AlexShortHub

A frontend design skill built by distilling nine external design/animation skills down to their operative rules, then organizing those rules into one adaptive workflow. It does not load every source's opinions on every project - it reads the brief, picks the smallest set of tools and rules that fit the theme, and builds with them.

The one thing every project shares: the output must not read as AI-generated. That means no default gradients, no badge/eyebrow clutter, no bullet-point walls standing in for real copy, no hand-rolled decorative SVG blobs, no dot-and-sparkline filler. [reference/anti-slop-checklist.md](reference/anti-slop-checklist.md) is mandatory reading before the first line of markup and the last gate before shipping.

## Workflow

Run these steps in order. Skip nothing, but keep each step to the size the brief actually needs - a one-page portfolio does not need the same depth of design-system research as a SaaS product site.

### 0. Check scope and mode

Read [reference/redesign-and-scope.md](reference/redesign-and-scope.md). If the request is a dashboard, a data table, a multi-step wizard, a code editor, a native mobile app, or a real-time collaborative UI, say so explicitly and point to the right tool instead of forcing this skill onto it - it's built for marketing pages, landing pages, portfolios, and content pages.

If this is a redesign rather than a greenfield build, detect which kind before anything else: preserve the existing brand, or a deliberate overhaul. Preserve means auditing the current brand tokens, IA, and SEO baseline first, and never silently changing URLs, nav labels, form field names, or the logo. Full detail in the same reference file.

### 1. Read the brief, state the direction

Before writing any code, read [reference/design-direction.md](reference/design-direction.md) and produce one line in the response:

> "Reading this as: `<page kind>` for `<audience>`, `<vibe>` language, targeting `<design system or custom aesthetic>`."

A bare topic and nothing else ("landing page for a dental clinic," "site for a coffee shop") is a complete brief, not an incomplete one. When there are no vibe words, references, or audience notes to go on, infer the read from the industry itself using [the category table](reference/design-direction.md#when-the-brief-is-just-a-topic) and proceed - do not ask a question just because the brief is short.

If the brief is genuinely ambiguous on a decision that changes the output materially (tone, whether to preserve an existing brand, one aesthetic vs. another), ask exactly **one** targeted question. Do not ask when you can confidently infer - most briefs, short or long, do not need a question.

### 2. Set the three knobs

Three numbers steer every layout, motion, and density decision downstream. Full inference table in [reference/design-direction.md](reference/design-direction.md#the-three-knobs).

- **Variance** (1 = perfectly symmetric grid, 10 = deliberately asymmetric/artsy)
- **Motion** (1 = static, 10 = cinematic/physics-driven)
- **Density** (1 = airy/gallery, 10 = packed/cockpit)

State the three numbers once, then build to them. Do not ask the user to tune them by hand - adjust conversationally if they push back on the result.

### 3. Pick the foundation - don't build what already has an official answer

Read [reference/layout-and-components.md](reference/layout-and-components.md). In short:

- If the brief matches a product with an official design system (enterprise SaaS, Shopify app, GOV/public-sector, a known component ecosystem), use that system's real package. Do not hand-roll its look.
- Otherwise: Tailwind + a real component source. Reach for **shadcn/ui** for primitives, **Componentry.dev** for polished pre-animated interactive components (only when the brief calls for something with real motion - a magnetic dock, particle text, liquid/ripple effects - not for plain buttons), and **Bklit UI** specifically for charts and data visualization (never hand-roll SVG charts when a themeable chart component exists).
- One component family per project. Never mix two icon libraries or two design systems in the same tree.

### 4. Pick the animation stack - match the tool to the job, not the reverse

Read [reference/motion-and-animation.md](reference/motion-and-animation.md) for the full decision framework (when to animate at all, easing, duration, and library routing). The short version:

| Need | Reach for |
|---|---|
| Hover/press/entrance micro-interactions, gestures, drag, scroll-linked reveals in a component-based app | **Motion.dev** (`motion/react`) |
| Scroll-driven timelines, pinning, scrubbing, SVG morphing, or anything framework-agnostic | **GSAP** + ScrollTrigger |
| A real 3D scene, product configurator, or interactive hero object, built visually rather than in code | **Spline** |
| A one-off transition on a static site with no JS framework | Plain CSS transitions/`@starting-style` |

Never load more than one animation library into a page. If Motion.dev already covers the interaction, do not also reach for GSAP "just in case."

### 5. Build

Apply [reference/typography-and-color.md](reference/typography-and-color.md) and [reference/layout-and-components.md](reference/layout-and-components.md) while writing markup and styles - they carry the concrete, numeric rules (type scale, contrast floors, spacing, hero constraints, section-repetition limits) that keep output specific rather than templated.

### 6. Verify once, in a bounded pass

Read [reference/qa-and-verification.md](reference/qa-and-verification.md). Build fully, inspect once (desktop + mobile together), fix everything the inspection surfaces, confirm with at most one more pass, then stop. Do not loop indefinitely polishing - that spends the user's time without spending it well.

The verification pass has two mandatory gates, run in this order:

1. **Anti-slop checklist** ([reference/anti-slop-checklist.md](reference/anti-slop-checklist.md)) - mechanical, binary, no judgment calls. Includes the copy self-audit: re-read every visible string for broken grammar, unclear referents, or forced-sounding phrasing before calling the copy done.
2. **Quality floor** ([reference/qa-and-verification.md](reference/qa-and-verification.md)) - contrast, states, responsive behavior, motion accessibility, copy.

Report what you found and fixed. If something in the checklist fired and you kept it anyway, say why - the brief can always override a default.

## Sources

This skill is an original synthesis, not a bundling of the source skills' text. Each source contributed rules and judgment calls, credited in [README.md](../../README.md#sources) at the repo root.
