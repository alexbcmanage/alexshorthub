# Typography and color

## Type

- Body copy measure: 65–75ch. Display size cap: 6rem. Tracking floor: -0.04em on display type.
- Scale: one font family for UI text, 3–4 sizes maximum, 2–3 weights. A second family (display or mono) only when the brief earns it.
- Run the actual copy at every breakpoint before shipping — a headline that fits in the design tool but wraps to four lines on a real viewport is a font-size error, not a copy-length error.
- **Hero headline: max 2 lines on desktop.** Subtext: max 20 words, max 3–4 lines. If the value proposition doesn't fit in 20 words of subtext, the value proposition is unclear — fix the message, not the limit.
- **Hero font scale and asset size are planned together.** A large hero image with a headline over six words should not start at the largest display size. Sensible default: `text-4xl` → `text-6xl` across breakpoints for most heroes; the largest sizes (`text-7xl`+) only for headlines of three to five words.
- **Italic descender clearance.** Italic display type on a word with a descender (y, g, j, p, q) needs `line-height` of at least 1.1, not `leading-none` — otherwise the descender clips.

### Font choice

- Inter is not the default. It's a fine choice when the brief explicitly wants neutral/standard, or the surface is accessibility-first/public-sector. Otherwise reach for something with more character first (a distinct grotesque or a brand-appropriate face).
- Serif is not the default "creative" or "premium" signal — that instinct is itself an AI tell. Use serif display type only when the brief names a serif explicitly, or the aesthetic is genuinely editorial, luxury, publication, or heritage, and you can state why this specific serif fits this specific brand. Everything else defaults to a sans display face.
- To emphasize a word inside a headline, use italic or bold of the *same* family. Injecting a different font family into one word for "visual interest" reads as amateur.
- A system fallback face (the platform default sans, Arial Black, Impact) is never the display voice of an own-world page — source and self-host a real face.

## Color

- One accent color per project, used everywhere it appears — a warm-neutral site doesn't get a blue CTA in section 7 and a teal badge in the footer. Lock the accent before building the second section.
- Saturation under 80% by default; reserve fully saturated color for the one thing that needs to grab attention.
- Contrast floor: body and placeholder text ≥4.5:1, large text ≥3:1. On a colored surface, tint secondary text from that hue rather than defaulting to plain gray.
- When a shadow is used, tint it toward the background hue rather than defaulting to pure black. A shadow needs both offset and blur — a zero-offset colored halo is decoration, not depth.
- One corner-radius scale per project (all-sharp, all-soft, or all-pill for interactive elements only) with a stated, consistent rule. Mixing radius scales without a rule (round buttons in an otherwise square layout) reads as broken, not eclectic.

### Avoiding the reflex palettes

Two color reflexes show up often enough in ungoverned output to be worth naming and routing around explicitly — not banning, since a brief can ask for either, but never defaulting into them:

- **The "AI purple/blue glow."** Automatic purple button glows, neon gradient accents with no basis in the brief. If the brand genuinely wants purple, execute with a flat, deliberate accent and a harmonized neutral base (zinc/slate/stone), not a generic glow.
- **The premium-consumer beige-and-brass reflex.** For cookware, wellness, artisan, or heritage-craft briefs, the reflex is warm cream/paper background + brass/clay/oxblood accent + espresso-dark text. It's recognizable precisely because it's the default reach, and it makes the brand invisible. Rotate into a real alternative unless the brief explicitly names this palette: cold-luxury silver/chrome, deep forest green with a bone neutral, true off-black with warm tan, a single saturated accent (cobalt, emerald, hot pink) against pure monochrome.

## Browser-default surfaces

Text selection color, the caret, custom scrollbars, focus rings, and tabular numerals in data all ship with generic browser defaults unless themed. Theming these is the cheapest signal that a page was actually designed rather than assembled from a template, and the detail most commonly skipped.
