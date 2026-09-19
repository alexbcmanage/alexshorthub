# Non-English briefs

Most of the rules in this skill were written against English copy and Latin type. When the brief is in another language, or the page is for readers of one, three of them stop working as written: the dash ban, the font rules, and the copy-length limits. Russian is the worked example below; the same checks apply to any language with its own punctuation and script.

Read this file at step 1 whenever the brief is not in English, and again before the copy self-audit.

## Decide the page language first

- The page copy is written in the language of the brief and the audience, not in English with a translation bolted on. Never ship English template phrases on a non-English page.
- Put the language on the document (`<html lang="ru">`). It drives hyphenation, quote glyphs, font selection, and screen readers.
- Say in the one-line design read which language the page is in, so the choice is visible.
- Invented names, cities, and currencies must be locale-appropriate (the fabricated-specificity rules already ask for this).

## Punctuation: the dash rule needs a locale exception

The em dash ban in [anti-slop-checklist.md](anti-slop-checklist.md) exists because English model output uses the em dash as a stylistic crutch. In Russian the dash is required grammar (between subject and predicate, in place of an omitted verb, in dialogue), so a page with zero dashes reads as wrong, not as clean.

The test for any dash in non-English copy: **would the language's punctuation rules require it here?**

- Required by grammar: keep it, typeset correctly.
- A stylistic pause, a headline separator, a "punchy aside": rewrite with a period, comma, or colon, exactly as in English. That is the tell the ban targets, and it applies in every language.

Russian typesetting, so the kept dashes and quotes are right:

- Dash `—` with a non-breaking space before it and a normal space after. Ranges use the short dash without spaces (`5–7 дней`, `2018–2026`) or are written out (`от 5 до 7 дней`). The English rule that ranges take a plain hyphen does not apply here.
- Quotes are `«ёлочки»`, nested `„лапки“`, never straight `"..."`.
- Non-breaking space after one- and two-letter prepositions and conjunctions (`в`, `к`, `с`, `и`, `на`), between a number and its unit (`5 кг`, `1 500 ₽`), and before a dash, so a line never ends on `в` or starts on `—`.
- Decimal comma, space as thousands separator, currency after the number. Format with `Intl.NumberFormat('ru-RU', ...)` and `Intl.DateTimeFormat('ru-RU', ...)` instead of by hand.
- Plurals have more than two forms (`1 посылка`, `2 посылки`, `5 посылок`). Use `Intl.PluralRules('ru')` or an i18n library; `count !== 1 ? 's' : ''` logic is wrong.

If Impeccable's `em-dash-overuse` detector fires on grammatical dashes, waive it with a stated reason (see gate 0 in [qa-and-verification.md](qa-and-verification.md)); do not delete correct punctuation to get a clean scan.

## Type: check the script before choosing the face

- **Confirm Cyrillic coverage before committing to a font.** Many display faces with character ship Latin only. A face that falls back to the browser default for Cyrillic mixes two fonts inside one headline, which is worse than choosing a plainer face that covers both scripts. Load the Cyrillic subset explicitly (Google Fonts `subset=cyrillic`, or `subsets: ['latin', 'cyrillic']` in `next/font`) and look at real Russian text at the real size, not at Latin specimen text.
- The "Inter is not the default" and "no system display face" rules still apply, but the shortlist is whatever covers the script well. If the only characterful faces you would pick lack Cyrillic, take a covered face and put the character into scale, weight, and layout instead.
- Check that the italic and the weights you plan to use exist in Cyrillic. Cyrillic italic letterforms differ from Latin and are absent from some families.
- The `-0.04em` tracking floor in [typography-and-color.md](typography-and-color.md) was set for Latin display type. Cyrillic is denser; tighten less, and judge at the real size.
- Avoid all-caps for long Russian words and for body text. Long words in capitals get hard to read fast.
- Latin brand names inside Cyrillic sentences: make sure the two scripts sit well together in the chosen face (x-height, weight) at heading size.
- Hyphenation: `hyphens: auto` on narrow body columns with the `lang` set, not on headlines. Use `text-wrap: balance` for headings.

## Length: re-test every fixed limit with the real translated copy

Russian and many other languages run longer than English for the same meaning. The hero limits (headline at most 2 lines, subtext at most 20 words), button widths, nav on one line, and tile heights were all tuned to English, so:

- Run the real final copy at every breakpoint (this is already a rule; here it is the main risk, not a formality).
- Size buttons and nav items to their content (`px-4 py-2`, never a fixed width). If the nav no longer fits on one line at `lg`, shorten labels before shrinking type.
- The 20-word subtext cap holds; the copy gets rewritten to fit it, not the cap raised.

## Copy: the filler rules apply in every language

The banned filler verbs ("Elevate," "Seamless," "Unleash") have direct equivalents in every language, and they read as generic there too. In Russian, calques and stock phrases such as «инновационное решение», «комплексный подход», «раскройте потенциал», «премиальный сервис», «мы заботимся о вас» say nothing; replace each with the concrete thing the product does. Do not translate an English tagline word for word; write the line the way a native speaker of the trade would say it.

Run the copy self-audit ([anti-slop-checklist.md](anti-slop-checklist.md#copy-self-audit-run-before-shipping-not-just-once-during-writing)) in the page language, and check grammar, case endings, and agreement in inserted values (numbers, city names) as part of it.

## Other scripts

- **Right-to-left languages:** use CSS logical properties (`margin-inline-start`, `padding-inline`, `border-inline-end`) instead of left/right, set `dir`, and mirror directional icons.
- **CJK and other scripts:** use UTF-8 throughout, test with real text, and expect different line-breaking and line-height needs.
- Do not let a decorative choice (a display face, a rotated label, negative tracking) decide whether the script renders correctly.

## What this file is based on

The script, RTL, `Intl`, and pluralization points follow Impeccable's hardening guidance. The Russian typography conventions and the dash exception are general typographic practice, not taken from any of the nine sources.
