# Anti-slop checklist

Mechanical, binary checks. Run before writing markup (so you don't build the thing you'll delete) and again before shipping (so nothing crept back in). Every item below is a default to avoid, not an absolute ban — a brief can earn any of them back explicitly. Reaching for one because it's the reflex is the failure; reaching for one because the brief asked is fine.

## Gradients

- No gradient text. Emphasis comes from weight, size, or color, never a `background-clip: text` rainbow.
- No default purple/blue "AI glow" — no automatic button glow, no mesh-gradient hero background, no radial-gradient blob standing in for a real visual. If the brand explicitly wants purple, execute it as a flat, intentional accent, not a glow.
- A gradient is allowed only when the brief's own palette calls for one and it does a specific job (a photo scrim, a genuine brand texture) — never as the default "make the hero less empty" move.

## Badges, pills, and eyebrows

- No small-caps "eyebrow" label above section headings (`SELECTED WORK`, `THE HARDWARE`, `FOUR COLORWAYS`) as a page-wide habit. Cap: at most one eyebrow per three sections, hero included in the count. The headline alone is enough; the section's position already tells the reader what it is.
- No feature-badge walls (a row of pill-shaped tags with no real filtering or state behind them).
- No status dot + label pattern standing in for real data ("● Live", "● 99.9% uptime") unless the number is real and updates.

## Dots, sparklines, and decorative micro-shapes

- No sparklines, progress rings, or soft-shadowed rounded rectangles used as decoration rather than as an actual chart of real data. If a chart is needed, use a real chart component (see [layout-and-components.md](layout-and-components.md)) bound to real or clearly-labeled sample data — never a fake trend line drawn to look busy.
- No dot-grid or dot-pattern backgrounds added purely to fill empty space.
- No pagination dots or carousel indicators added by default — only when there's an actual carousel and the dots communicate real position.

## Unnecessary text

- No hero stack beyond: one eyebrow OR brand strip (optional, pick zero or one), one headline (max 2 lines), one subtext (max 20 words, max 4 lines), CTAs (one primary, at most one secondary). No tiny tagline under the CTAs, no trust micro-strip, no pricing teaser, no feature bullet list stuffed into the hero — those get their own section below the hero.
- No duplicate CTA intent on one page. "Get in touch," "Contact us," "Let's talk," and "Start a project" are the same intent — pick one label and reuse it everywhere (nav, hero, footer).
- No restating in a subheading what the heading already said. No "In summary" / "In conclusion" sections on a marketing page.
- No logo-wall labels under each logo ("Stripe — payments", "Vercel — hosting"). The logo is the credibility; the category label adds nothing.
- Cut copy hard: read every sentence and ask whether removing it loses information the reader needs. If not, cut it.

## Hand-rolled and generic SVG

- Never hand-draw icon paths from scratch. Use one real icon library (Phosphor, Radix Icons, Tabler, Lucide) per project, one stroke weight, consistently.
- Never use a plain geometric mask (circle/polygon/radial-gradient cutout) as a stand-in for a photographic subject's edge — it reads worse than no mask at all. Use a real alpha matte or cut-out asset, or skip the effect.
- Never fill an empty hero with a hand-rolled abstract SVG blob shape. If there's no real product shot, 3D render, or photograph available, say so explicitly and leave a labeled placeholder rather than shipping a blob.
- Div-based fake product previews (rectangles standing in for a screenshot, a fake terminal window, a fake task list) are a tell. Use a real screenshot, a generated image, an actual mini-render of the real UI, or skip the preview.
- Invented brand names still need a real mark: a simple monogram or two-letter ligature as inline SVG, not a styled `<span>` wordmark pretending to be a logo.

## Layout templates

- No page built entirely from same-size cards of icon + heading + text. Cards earn their place when elevation communicates real hierarchy; otherwise group with spacing, a top border, or a divider.
- No hero-metric template (big number, small label, a row of supporting stats, one accent color) unless the numbers are real and the brief is genuinely metrics-led.
- No section numbering (01 / 02 / 03) unless the sequence itself is information the reader needs to track.
- No more than two consecutive sections using the same layout family (e.g., image-left/text-right, then text-left/image-right, then a third of the same shape). Break the third one with a full-width section, a grid, or a different composition.
- No centered hero by default once variance is above the low end — force an asymmetric or split composition unless the brief is a manifesto/announcement where the centered message is the whole point.

## Emoji and unicode glyphs as icons

- No emoji or unicode glyphs standing in for a real icon. Use the project's icon library. Emoji are fine only when the brief is explicitly playful/chat/social-native, and even then sparingly.

## Fonts

- Inter is not the default. Reach for it only when the brief explicitly wants a neutral/standard feel or is accessibility-first/public-sector.
- Serif is not the default "creative" or "premium" move. Only use serif display type when the brief names one explicitly, or the aesthetic is genuinely editorial/luxury/heritage and you can say why this specific serif fits this specific brand.

## Running the check

Before shipping, count instances of each pattern above across the built page. Any count that exceeds the stated cap (eyebrows, consecutive same-family sections, duplicate CTA intents) is a fail — fix it, don't rationalize it. Everything else is a scan-and-confirm: if you don't see it, move on.
