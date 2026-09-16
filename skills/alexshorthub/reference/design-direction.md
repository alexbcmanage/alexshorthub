# Design direction

## Read the brief before deciding anything

Pull these signals out of the request before generating anything:

1. **Page kind** — landing (SaaS / consumer / agency / event), portfolio (developer / designer / studio), redesign (preserve vs. overhaul), editorial/blog, product UI/dashboard.
2. **Vibe words** the user actually used — "minimalist," "calm," "Linear-style," "brutalist," "premium," "playful," "serious B2B," "editorial," "dark tech." These outrank your own taste.
3. **Reference signals** — URLs, screenshots, named competitors or products.
4. **Audience** — a procurement panel, a design-conscious consumer, a recruiter, a public-sector citizen. The audience picks the aesthetic, not you.
5. **Existing brand assets** — logo, color, type, photography. For a redesign these are starting material, not optional input; treat the old look as evidence, not as a blank slate to override.
6. **Quiet constraints that override aesthetic preference** — accessibility-first audiences, regulated industries, trust-first commerce, kids' products, public-sector services.

State the read in one line before building:

> "Reading this as: `<page kind>` for `<audience>`, `<vibe>` language, targeting `<design system or custom aesthetic>`."

Ask exactly one clarifying question only when the read genuinely forks into two different builds. Otherwise commit to the read and move.

## What surface is this — the four modes

Choose per-surface, not per-product. A tool's own marketing page is Persuade even if the tool itself is Operate; a fashion brand's documentation is Read even if the brand is Experience everywhere else.

- **Persuade** — the visitor decides and acts. Landing pages, marketing, campaigns, pricing. Design is the product; earn the attention and the click.
- **Operate** — the visitor completes a task. Dashboards, editors, admin, settings. Scanability and consistency outrank expression; brand lives in the details, not the layout.
- **Read** — the visitor understands something. Docs, articles, guides, changelogs. Structure for comprehension first, then make staying worth it.
- **Experience** — the visitor is inside the work. Portfolios, galleries, showcases. The artifact leads from the first viewport; the interface recedes.

The mode changes what "good" means for hierarchy and restraint — an Operate surface with Persuade-level visual noise is broken, and a Persuade surface with Operate-level restraint is forgettable.

## The three knobs

Set these once, from the brief, and build to them. They gate every layout, motion, and density call downstream.

- **Variance** — 1 = perfectly symmetric grid, 10 = deliberately asymmetric/artsy.
- **Motion** — 1 = static, 10 = cinematic/physics-driven.
- **Density** — 1 = airy/gallery, 10 = packed/cockpit.

Baseline for an unspecified marketing site: **variance 7, motion 6, density 4**.

| Brief signal | Variance | Motion | Density |
|---|---|---|---|
| Minimalist / calm / editorial / Linear-style | 5–6 | 3–4 | 2–3 |
| Premium consumer / Apple-like / luxury brand | 7–8 | 5–7 | 3–4 |
| Playful / experimental / agency / awwwards-style | 9–10 | 8–10 | 3–4 |
| Trust-first / public-sector / regulated / accessibility-critical | 3–4 | 2–3 | 4–5 |
| Dashboard / data-dense product UI | 4–5 | 2–3 | 6–8 |
| Redesign, preserve identity | match existing | +1 | match existing |
| Redesign, deliberate overhaul | +2 | +2 | match existing |

Never invent new knob names mid-project. Refer back to these three, and state the numbers once in the response rather than re-deriving them per section.

## Refinement vs. redesign

- **Refinement** keeps the incumbent identity, copy, and everything outside scope. Don't replace factual copy or invent claims without asking.
- **Redesign** keeps product truth, content, and constraints, but treats the old visual world as evidence and anti-reference — pick a real replacement direction rather than splitting the difference between old and new.
- A missing design doc alone does not make a project greenfield. Look at what already exists before deciding whether to preserve, extend, or replace it.

## Anti-default discipline

The read exists specifically to route around what an unprompted model reaches for by default: AI-purple gradients, a centered hero over a dark mesh background, three identical feature cards, glassmorphism applied to everything, Inter paired with slate-900 text. None of these are banned outright — they're the reflex. The three knobs and the read above should already be steering away from them before the anti-slop checklist even runs as a final gate.
