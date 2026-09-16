# Layout and components

## Foundation: don't rebuild what already has an official answer

Check the brief against a real design system before writing custom CSS:

| Brief reads as… | Use the official package |
|---|---|
| Enterprise SaaS / Microsoft-adjacent | Fluent UI (`@fluentui/react-components`) |
| Material-flavored Google-ish product | Material Web (`@material/web`) + Material 3 tokens |
| IBM-style enterprise analytics | Carbon (`@carbon/react`) |
| Shopify app surface | Polaris |
| Atlassian/Jira-style product | Atlaskit |
| GitHub-style devtool | Primer |
| UK public-sector service | GOV.UK Frontend |
| US public-sector / trust-first | USWDS |

Never hand-recreate one of these systems' CSS by hand, never import its tokens and then override most of them, and never mix two systems in one tree.

When the brief is an aesthetic rather than a system (glassmorphism, bento grids, brutalism, editorial, dark-tech), there is no official package - build with native CSS/Tailwind honestly, and say in comments what's borrowed inspiration versus your own execution.

## Default stack when nothing more specific applies

- Tailwind (latest major) for utility styling.
- One icon library for the whole project - Phosphor, Radix Icons, or Tabler are safe defaults. Never hand-draw icon paths.
- **shadcn/ui** for owned, customizable primitives (you get the source, not a black box).
- **Componentry.dev** when the brief specifically needs a component with real interactive motion already built - a magnetic dock, particle-text effect, image-ripple hover, liquid/WebGL surface - rather than hand-rolling a bespoke interaction from scratch. Install via its shadcn-CLI-compatible flow, keep the source editable, and only reach for it when plain CSS/Motion.dev would clearly be more work for the same result.
- **Bklit UI** specifically for charts and data visualization (area, bar, line, composed, scatter, candlestick, pie, radar, gauge, funnel, sankey, choropleth). Install via its shadcn registry (`npx shadcn@latest add @bklit/<chart>`), theme through its CSS variables, never hand-roll an SVG chart when a themeable component covers the case.
 - Compose root-first: series, axes, grid, and tooltip are all children of the root chart component (`<LineChart><Grid /><Line dataKey="users" /><XAxis /><ChartTooltip /></LineChart>`), never a bare `<div>` wrapping loose series and axis components outside a chart context.
 - Put `Grid` before the series children so lines/bars render on top of the gridlines, not under them.
 - Theme with the exported `chartCssVars` / `--chart-1`…`--chart-5` tokens, not raw hardcoded colors - this is what makes the chart follow the page's light/dark theme automatically.
 - Default enter animation is ~1100ms; to replay it after data changes, remount with a new `key` or change the `revealSignature` prop rather than fighting the internal animation state.

One component family per project. Don't mix two icon sets or import components from two unrelated design systems into the same page.

## Hero

- Must fit in the initial viewport. Headline max 2 lines, subtext max 20 words, CTAs visible without scrolling.
- Top padding capped around `pt-24` (~6rem) at desktop - more than that and the hero content reads as a layout bug, not intentional breathing room. If it needs more air, scale the font or the asset, not the padding.
- Text stack, in order, max 4 elements: optional eyebrow or brand strip (pick zero or one, not both), headline, subtext, CTAs (one primary, at most one secondary). No trust micro-strip, no pricing teaser, no bullet list crammed into the hero - those get their own section directly below.
- A logo wall ("used by," "trusted by") lives under the hero, not inside it.
- The hero needs a real visual: a photograph, a generated image, a product render, or an actual 3D scene. Text over a gradient blob is a placeholder, not a hero.

## Navigation

- Renders on one line at desktop. If items don't fit at the `lg` breakpoint, condense labels or move overflow to a menu - a two-line nav is broken, not dense.
- Height capped around 64-80px. No oversized "agency" nav bars eating a large share of the viewport.

## Section rhythm

- Once a layout family is used for a section (three-column cards, full-width quote, split image/text), it can repeat once more at most before the page needs a different family. A page with eight sections should draw from at least four different layout families.
- Max two consecutive sections in an alternating image/text zigzag before breaking the pattern with a full-width section, a grid, or a vertical stack.
- If a section has both a large headline and a smaller explainer paragraph side by side ("split header"), only do this when the second column carries a real visual or interactive element - not filler text. Otherwise stack headline and body vertically at one measure.
- Bento/feature grids have exactly as many cells as there is content for - no empty filler tile. At least a couple of cells in any multi-cell grid should carry real visual variation (an image, a brand-consistent pattern, a tint), not six identical white cards with text.

## Cards and containers

- Cards earn their place when elevation communicates real hierarchy. Otherwise group content with spacing, a single top border, or a divider - never nest a card inside a card.
- For dense data surfaces, plain layout beats generic card containers; let the data breathe without a container drawn around every metric.

## Image and asset strategy

Landing pages and portfolios are visual products - a text-only page with div-shaped "fake screenshots" is unfinished work, not minimalism.

1. Use an image-generation tool when one is available, for hero photography, product shots, and mood images at the section's actual aspect ratio.
2. Otherwise use real photography (licensed stock, brand-provided URLs, or clearly-seeded placeholder photography) rather than filling space with shapes.
3. If neither is possible, say so explicitly and leave a labeled placeholder (e.g. an HTML comment naming the needed asset and size) rather than shipping a hand-rolled SVG illustration or a div-based fake product preview.

For social-proof logo walls, use real SVG marks (a logo CDN, or the project's actual brand assets), ensure they render in both light and dark themes, and never print a category label under each logo.

## Interactive states

Every interactive surface needs its full state set, not just the happy path: hover, active/pressed, disabled, loading, error, empty. Skeleton loaders should match the final layout's shape rather than a generic spinner. Empty states should say how to populate them, not just "no results."

## Forms

Label above the input, helper text present in markup even when visually subtle, error text below the input. Never use a placeholder as the only label.
