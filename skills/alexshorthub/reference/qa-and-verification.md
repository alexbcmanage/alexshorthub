# QA and verification

## Verify in one bounded pass, not a loop

Build the full surface first. Then inspect once - desktop and mobile together, not as separate trips. Fix everything that inspection surfaces in one batch. Confirm with at most one more pass. Stop.

Open-ended self-review after that point burns time re-checking things that were already fine and rarely catches anything the first pass missed. If something is still wrong after the second pass, say so explicitly rather than continuing to iterate silently - report it as a known gap.

## Gate order

0. **Automated detector, when it can run** (optional, one run, part of the same bounded pass). Impeccable ships a standalone CLI with 61 deterministic anti-pattern rules (side-tab borders, gradient text, bounce easing, dark glows, line length, cramped padding, skipped headings, small touch targets, and more). Run it once against the built source or the served page instead of eyeballing what a scanner does better:
   - `npx impeccable detect src/` (a directory), `npx impeccable detect index.html`, or `npx impeccable detect http://localhost:3000` (a URL; needs an installed Chrome, Chromium or Edge). Add `--json` for machine-readable output.
   - Exit `0` = scan finished with no primary findings, `2` = finished with findings, `1` = a target could not be scanned. Findings print to stderr.
   - The first run may download a platform binary into `~/.impeccable/bin/`. If there is no network or the user has not agreed to a download, skip this gate and say so in the report; do not pretend it ran.
   - A clean run is evidence, not proof. It does not replace inspecting the rendered page at desktop and mobile.
   - A finding the brief deliberately earned (a named brand font flagged as overused, a language whose punctuation trips a copy rule) is waived explicitly and reported: an inline `<!-- impeccable-disable <rule-id>: <reason> -->` in that file, or `npx impeccable ignores add-value <rule-id> <value> --reason "..."`. Never silence a rule just to get a clean exit code.
1. **Anti-slop checklist** ([anti-slop-checklist.md](anti-slop-checklist.md)) next. It's mechanical and binary - run it before the quality floor below so you're not polishing a pattern you're about to delete. It also covers what a scanner cannot see: copy quality, fabricated specificity, and hero and page-chrome tells.
2. **Quality floor** (this file) last, on what survives gates 0 and 1.

## Quality floor

**Contrast.** Body and placeholder text ≥4.5:1, large text ≥3:1. Verify on every background color actually used, not just the default surface.

**States.** Every interactive element has hover, active/pressed, disabled, loading, and error states implemented - not just the happy path. Empty states say how to populate them.

**Responsive.** Real content (not lorem ipsum) run at every breakpoint declared. No horizontal scroll from overflow. Touch targets at least 44×44px. No layout that only works at the exact viewport width used while building it.

**Motion accessibility.** Every animation has a `prefers-reduced-motion` path that still communicates the state change; a global `animation: none` that silently drops feedback is a fail, not a pass.

**Copy.** Controls name their action ("Save changes," not "Submit"). Errors name the problem and the recovery, not an error code. No placeholder text standing in for a label.

**Coverage.** Every requirement in the brief is present in the build and findable within seconds - nothing silently dropped because it was inconvenient to fit into the chosen layout.

**Browser-default surfaces.** Text selection color, caret, scrollbar, and focus ring are themed to the palette rather than left at browser defaults - this is the cheapest tell that a page was assembled rather than designed, and the detail skipped most often.

## Report what the pass found

State what the verification pass caught and fixed, not just a final "looks good." If the anti-slop checklist flagged something and it was kept deliberately (the brief explicitly asked for a gradient, say), name that decision instead of silently overriding the checklist. A verification pass that reports nothing found on a first build is a sign the pass didn't actually run - real builds almost always have at least a contrast or state gap on the first inspection.

## Mechanical pre-ship checklist

The prose gates above cover the reasoning; this is the fast, scannable pass over the highest-signal binary checks pulled from every reference file. If any box fails, the build is not done - fix it, don't rationalize it.

- [ ] Zero decorative em dashes anywhere visible on the page (headline, body, quote, caption, alt text, button). In non-English copy, only dashes the language's punctuation requires remain ([non-english-briefs.md](non-english-briefs.md)).
- [ ] One accent color, one corner-radius system, one light/dark theme, one copy register - each used identically across every section.
- [ ] Hero fits the viewport unscrolled: headline ≤2 lines, subtext ≤20 words, primary CTA visible, top padding ≤ ~6rem.
- [ ] No duplicate CTA intent anywhere on the page (nav, hero, footer all say the same thing for the same action).
- [ ] No eyebrows unless the surface or the brief needs them, and never more than `ceil(sections / 3)`; no section-number eyebrows or staged-progress labels.
- [ ] Non-English page only: `lang` set, chosen fonts confirmed to cover the script, real copy re-tested at every breakpoint ([non-english-briefs.md](non-english-briefs.md)).
- [ ] Detector (gate 0) run and clean, or every waived finding named with its reason, or the gate explicitly reported as skipped.
- [ ] No more than two consecutive sections share a layout family.
- [ ] Every CTA's text is readable against its own background (no white-on-white, WCAG AA 4.5:1 minimum).
- [ ] Every ScrollTrigger/GSAP pin uses `start: "top top"` (or an equivalent verified start), not a default that fires mid-reveal.
- [ ] No `window.addEventListener('scroll', ...)` or scroll position written into framework state anywhere in the code.
- [ ] Every animation above the low end of the motion knob has a working `prefers-reduced-motion` fallback that still shows the state change.
- [ ] Real images or a labeled placeholder - no div-based fake screenshots, no hand-rolled decorative SVG blobs.
- [ ] Icons come from exactly one library; no hand-drawn icon paths.
- [ ] Redesign only: URL slugs, nav labels, form field names, and the logo are unchanged unless the user explicitly approved changing them.
- [ ] Copy self-audit run (see [anti-slop-checklist.md](anti-slop-checklist.md#copy-self-audit-run-before-shipping-not-just-once-during-writing)) - no broken or AI-sounding strings left in visible copy.

## Scope discipline

Verification checks what was built against the brief and the checklists above - it does not become an opportunity to add unrequested features, restructure sections that weren't in scope, or "improve" copy the user didn't ask you to touch. Flag opportunities if you see them; don't act on them unasked.
