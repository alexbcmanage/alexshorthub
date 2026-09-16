# Redesign protocol and scope

## Detect the mode first

Misreading which of these three a request is drives most bad redesign output - figure this out before touching anything:

- **Greenfield**: no existing site, or a full overhaul has been explicitly approved. Start from the dial baseline in [design-direction.md](design-direction.md).
- **Redesign, preserve**: modernize without breaking the brand. Audit first, extract the brand's real tokens, evolve gradually.
- **Redesign, overhaul**: a new visual language on top of existing content. Treat the visuals as greenfield; preserve content and information architecture.

If it's genuinely ambiguous which of these applies, ask exactly one question: "Should this preserve the existing brand, or are we starting visually from scratch?" Don't guess on this one - it changes almost every downstream decision.

## Audit before touching anything

For any redesign (preserve or overhaul), document the current state before proposing changes:

- **Brand tokens actually in use** - primary/accent colors, type stack, logo treatment, corner radii.
- **Information architecture** - page tree, primary nav, the paths that actually convert.
- **Content inventory** - what's doing real work, what's filler.
- **Patterns worth preserving** - a signature interaction, a recognizable hero, an established copy voice.
- **Patterns worth retiring** - AI-slop tells (see [anti-slop-checklist.md](anti-slop-checklist.md)), broken layouts, dead links, generic stock imagery, performance traps.
- **A dial reading of the existing site** (see [design-direction.md](design-direction.md#the-three-knobs)) - infer its current variance/motion/density. That's the actual starting point, not the fresh-project baseline.
- **The SEO baseline** - current ranking pages, meta titles, structured data, OG cards. Losing organic traffic is the single biggest risk in a redesign, and it's avoidable.

## What a "preserve" redesign never changes without explicit approval

- URL structure and route slugs.
- Primary navigation labels.
- Form field names or order (breaks analytics and browser autofill).
- The brand logo or wordmark.
- Existing legal, consent, or cookie copy.
- Copy voice - a visual refresh is not license to rewrite content unless the user asked for that too.
- Existing accessibility wins - don't regress focus states, alt text, keyboard navigation, or contrast while "modernizing" the visuals.
- Analytics event names tied to button/section/field IDs.

## Modernization levers, in priority order

Apply these in order and stop once the brief is satisfied - don't automatically escalate to a full rebuild:

1. **Typography refresh** - the biggest visual lift for the least structural risk.
2. **Spacing and rhythm** - larger section padding, corrected vertical rhythm.
3. **Color recalibration** - desaturate, unify neutrals, keep the existing brand accent.
4. **Motion layer** - add motion-knob-appropriate micro-interactions to components that already exist.
5. **Hero and key-section recomposition** - restructure the top of the page using the layout patterns in [layout-and-components.md](layout-and-components.md).
6. **Full block replacement** - reserved for a block that's genuinely unsalvageable, not a default starting point.

## Targeted evolution vs. full redesign

- Information architecture, content, and SEO are all sound → **targeted evolution** (levers 1-4). This captures most of the visible improvement at a fraction of the risk of a rebuild.
- The visual debt is structural (broken IA, no consistent design system, broken mobile) → **full redesign**, with strict content preservation per the rules above.
- The brand itself is changing → **greenfield**. Treat the old site purely as reference material, not as a base to edit.

## Out of scope - say so and point elsewhere

This skill is built for marketing pages, landing pages, portfolios, and about/content pages. It is not the right tool for:

- **Dashboards, dense product UI, and admin panels.** Reach for a real design system instead (Fluent, Carbon, Atlassian, Polaris - see [layout-and-components.md](layout-and-components.md)).
- **Data tables.** Use TanStack Table or AG Grid rather than hand-building sortable/filterable table UI.
- **Multi-step forms and wizards.** These need form-flow-specific patterns this skill doesn't cover.
- **Code editors.** Use Monaco or CodeMirror with their own official theming.
- **Native mobile apps.** Apply Apple HIG or Material Design directly rather than translating web patterns.
- **Real-time collaborative UI** (presence indicators, live cursors, operational-transform-aware interfaces) - a different problem class with its own patterns.

When a request falls into one of these categories, say so explicitly, point to the right tool, and apply only the parts of this skill that genuinely transfer (e.g., a SaaS product's own marketing page is in scope even though its dashboard is not).
