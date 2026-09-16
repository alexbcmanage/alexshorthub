# Anti-slop checklist

Mechanical, binary checks. Run before writing markup (so you don't build the thing you'll delete) and again before shipping (so nothing crept back in). Every item below is a default to avoid, not an absolute ban - a brief can earn any of them back explicitly. Reaching for one because it's the reflex is the failure; reaching for one because the brief asked is fine.

## Typographic tells

- **No em dash (`—`) or en dash used as a separator (`–`), anywhere the user will see it** - headline, eyebrow, pill, button, body copy, quote, attribution, caption, alt text. This is the single most common model-written tell; there is no "used sparingly" exception. Rewrite with a period, a comma, a colon, or two sentences. Ranges (`2018-2026`, `€40-80k`) use a plain hyphen. If a single em dash survives to the final page, the copy pass isn't done.
- No middle-dot (`·`) used as the default separator for everything ("foo · bar · baz · qux"). At most one per line in a metadata strip; prefer line breaks, hairlines, or columns for anything longer.
- No `<br>`-broken, italicized headline split as a default "design move" ("for thirty\<br\>*years.*"). Headlines read naturally first; get typographically clever only when the brief specifically calls for it.
- No vertical rotated text ("INDEX OF WORK, 2018-2026" rotated 90°) unless the brief is explicitly agency/experimental and the rotation serves the actual composition.
- No decorative hairline grid lines added purely to make the page "feel designed." A line earns its place by organizing real content.

## Fabricated specificity ("Jane Doe" effect)

- No generic placeholder names ("John Doe," "Sarah Chan," "Jack Su") in testimonials, team sections, or sample data. Use specific, realistic, locale-appropriate names.
- No generic egg/silhouette avatars or default icon-library "user" glyphs standing in for people. Use a believable photo placeholder or a deliberately styled initial/monogram instead.
- No suspiciously round or suspiciously precise fake numbers (`99.99%`, `50%` uptime, `1234567` users) invented to look like data. Real data is fine; explicitly labeled mock data (`<!-- mock -->`, "example") is fine; invented engineering-precision numbers the brand never claimed are not.
- No startup-slop invented brand names ("Acme," "Nexus," "SmartFlow," "Cloudly") for placeholder companies - invent a name that sounds like it belongs to a real company in that specific industry.
- No filler verbs standing in for a real claim: "Elevate," "Seamless," "Unleash," "Next-Gen," "Revolutionize," "Empower." Say what the product actually does.

## Hero and page-chrome tells

- No version/status labels in the hero (`V0.6`, `BETA`, `ALPHA`, `INVITE-ONLY PREVIEW`, `EARLY ACCESS`) unless the brief is genuinely about a product launch or preview status.
- No brand-plus-index sub-eyebrow ("Marrow · No. 01 · The 6-Quart") as a default hero device.
- No locale/time/weather strip ("LIS 14:23 · 18°C", a city name in the hero, coordinates in the footer) unless the brief is a genuinely globally-distributed studio, a travel brand, or a real physical venue. A single address line in the footer is fine; an atmospheric locale strip is not.
- No scroll cue ("Scroll," "↓ scroll to explore," an animated mouse-wheel icon). If the visitor hasn't scrolled yet, they're looking at the hero - they know scrolling exists.
- No decoration text strip at the hero's bottom edge ("BRAND. MOTION. SPATIAL.", "TYPE / FORM / MOTION") unless it's a real, navigable sticky bar or carries genuine status information.
- No "quietly trusted by" / "quietly in use at" social-proof phrasing. Say "Trusted by," "Used at," "Customers include," or drop the heading and let the logos speak.

## Badges, pills, and eyebrows

- Small-caps "eyebrow" labels above section headings, at most **one per three sections** (hero counts as one). Count the actual instances of an uppercase/tracked micro-label above a headline across the page; if the count exceeds `ceil(sections / 3)`, cut some. The headline alone is usually enough - the section's position already tells the reader what it is.
- No section-number eyebrows (`00 / INDEX`, `001 · Capabilities`, `06 · how it works`) or `01 / 4`-style pagination captions on tiles - if the reader can count, they don't need the label.
- No generic staged-progress labels ("Step 1 / Step 2 / Step 3," "Phase 01 / Phase 02," "Stage One / Stage Two"). Use the actual action as the label ("Install," "Configure," "Ship"), not a numbered wrapper around it.
- No pill/label overlays on photographs (`Plate · 02`, `Field notes - journal`). Either let the image stand alone or caption it directly below, outside the image.
- No invented photo-credit captions on stock or generated imagery ("Field study no. 12 · Ines Caetano"). Only caption a photo when a real photographer is being credited with permission; otherwise skip the caption or use one plain functional line ("The 6-quart, in sage.").
- No feature-badge walls - a row of pill-shaped tags with no real filtering or state behind them.

## Dots, sparklines, and decorative micro-shapes

- No decorative colored status dot in front of nav items, list rows, or badges by default. A dot earns its place only when it reflects real, live state (an actual server-status indicator, a genuine availability flag) - and even then, at most one per page section.
- No sparklines, progress rings, or soft-shadowed rounded rectangles used as decoration rather than as a real chart of real data. If a chart belongs on the page, use a real chart component bound to real or clearly-labeled sample data (see [layout-and-components.md](layout-and-components.md)) - never a fake trend line drawn to look busy.
- No comparison bars built from a filled background track with a partial fill on top (dashboard-style progress bars used as marketing comparison visuals). Prefer a number plus a small icon, or a thin inline bar with no background track.
- No dot-grid or dot-pattern background added purely to fill empty space.
- No pagination dots or carousel indicators by default - only when there's a real carousel and the dots communicate real position.

## Unnecessary text

- No hero stack beyond: one eyebrow OR brand strip (optional, pick zero or one), one headline (max 2 lines), one subtext (max 20 words, max 4 lines), CTAs (one primary, at most one secondary). No tiny tagline under the CTAs, no trust micro-strip, no pricing teaser, no feature bullet list stuffed into the hero - those get their own section below the hero.
- No duplicate CTA intent on one page. "Get in touch," "Contact us," "Let's talk," and "Start a project" are the same intent - pick one label and reuse it everywhere (nav, hero, footer).
- No micro-meta sentence sitting under an eyebrow or section heading just to sound thoughtful ("Each of these is a feature we ship today, not a roadmap promise..."). Eyebrow (if any) plus headline plus body is enough.
- No restating in a subheading what the heading already said. No "In summary" / "In conclusion" sections on a marketing page.
- No logo-wall labels under each logo ("Stripe - payments," "Vercel - hosting"). The logo is the credibility; the category label adds nothing.
- No floating explainer paragraph in the corner of a section header with no clear alignment to anything (a small paragraph parked top-right next to a big left-aligned headline). Either put the explainer directly under the headline, or build a deliberate two-column header - not a stray corner block.
- No version footer on a marketing page (`v1.4.2`, `Build 0048`, `last sync 4s ago · main`) - that's dev-tool chrome, not landing-page content.
- No live-stock counter ("Reservation 412 of 800") unless the brief is a genuine limited-run offer backed by real numbers.
- Cut copy hard: read every sentence and ask whether removing it loses information the reader needs. If not, cut it.

## Content density

- No 20-row data table, 30-row award list, or full pricing matrix dropped onto a marketing page. Show the top 3-5 highlights with a link to the full list, or move the data to its own page.
- Once a list passes 5 items, a plain bulleted `<ul>` or a `divide-y` row list is the lazy default - reach for a card grid, tabs/accordion, scroll-snap pills, a carousel, or a marquee instead, matched to what the list actually is.
- A long specification table with a border under every row (materials, dimensions, warranty terms) is a recognizable AI default for hardware/cookware/apparel briefs. Use a small card grid (one card per spec, with a display-sized value), grouped clusters with one divider per cluster, or a featured-vs-rest split instead.
- Quotes and testimonials: max 3 lines of quote body, real typographic quote marks (not straight ASCII), attribution as name + role + company (never a bare name), no em dash inside the quote.

## Hand-rolled and generic SVG

- Never hand-draw icon paths from scratch. Use one real icon library (Phosphor, Radix Icons, Tabler, Lucide) per project, one stroke weight, consistently.
- Never use a plain geometric mask (circle/polygon/radial-gradient cutout) as a stand-in for a photographic subject's edge - it reads worse than no mask at all. Use a real alpha matte or cut-out asset, or skip the effect.
- Never fill an empty hero with a hand-rolled abstract SVG blob shape. If there's no real product shot, 3D render, or photograph available, say so explicitly and leave a labeled placeholder rather than shipping a blob.
- Div-based fake product previews (rectangles standing in for a screenshot, a fake terminal window, a fake task list, a fake version footer inside the fake screenshot) are the single most common visual tell. Use a real screenshot, a generated image, an actual mini-render of the real UI, or skip the preview.
- Invented brand names still need a real mark: a simple monogram or two-letter ligature as inline SVG, not a styled `<span>` wordmark pretending to be a logo.

## Layout templates

- No page built entirely from same-size cards of icon + heading + text. Cards earn their place when elevation communicates real hierarchy; otherwise group with spacing, a top border, or a divider.
- No three-identical-cards-in-a-row feature layout as the page's only structural idea. Vary it: an asymmetric grid, a zigzag (capped, see below), a scroll-pinned sequence, or a horizontal-scroll alternative.
- No hero-metric template (big number, small label, a row of supporting stats, one accent color) unless the numbers are real and the brief is genuinely metrics-led.
- No more than two consecutive sections using the same layout family (e.g., image-left/text-right, then text-left/image-right, then a third of the same shape). Break the third one with a full-width section, a grid, or a different composition.
- No centered hero by default once variance is above the low end (see [design-direction.md](design-direction.md#the-three-knobs)) - force an asymmetric or split composition unless the brief is a manifesto/announcement where the centered message is the whole point.
- No "left big headline, right small explainer paragraph" section header unless the right column carries a real visual or interactive element. Otherwise stack headline and body vertically at one measure.
- Page keeps **one** light/dark theme throughout. No section flips to the inverted mode mid-scroll unless the brief explicitly wants a deliberate one-time theme-switch device as its own composition beat.
- One copy register for the whole page - don't mix technical-mono metadata, editorial prose, and punchy marketing copy in the same composition unless the brand voice explicitly calls for that mix.

## Emoji and unicode glyphs as icons

- No emoji or unicode glyphs standing in for a real icon. Use the project's icon library. Emoji are fine only when the brief is explicitly playful/chat/social-native, and even then sparingly.

## Fonts

- Inter is not the default. Reach for it only when the brief explicitly wants a neutral/standard feel or is accessibility-first/public-sector.
- Serif is not the default "creative" or "premium" move. Only use serif display type when the brief names one explicitly, or the aesthetic is genuinely editorial/luxury/heritage and you can say why this specific serif fits this specific brand.

## Copy self-audit (run before shipping, not just once during writing)

Re-read every visible string on the built page - headlines, subheads, eyebrows, button labels, body copy, captions, alt text, footer, error messages - and flag anything that is:

- Grammatically broken or missing a clear referent ("free on its past," "we plan to stay that way" with nothing established before it).
- A forced metaphor or cute wordplay that doesn't actually track.
- Written in a tone that performs thoughtfulness rather than saying something plain ("field notes," "on our desks," mock-humble asides).

Rewrite every flagged string. When in doubt, replace it with a plain, functional sentence - boring, correct copy beats clever, broken copy.

## Running the check

Before shipping, count instances of each capped pattern above (eyebrows, consecutive same-family sections, duplicate CTA intents, dots) across the built page. Any count that exceeds the stated cap is a fail - fix it, don't rationalize it. A single visible em dash anywhere is also a fail on its own, no count needed. Everything else is a scan-and-confirm: if you don't see it, move on.
