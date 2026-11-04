# ROVELLC S312 — Mobile UX/UI functional audit vs MyCabin Living 100
**Audit ID:** UX-S312-MOBILE-20261104
**Date:** 2026-11-04, Europe/Riga
**Auditor scope:** browser-simulated responsive functional/DOM QA and expert heuristic comparison, not real-device certification or user study.
**Target:** https://fibo-etf-atelier-owner-preview.onrender.com/
**Comparison:** https://www.mycabin.lv/konfigurators?model=living-100&market=LV
**Preview commit:** `f4a987e04f0d468d2f5e3015d541b9fe69ecebaa` / Render deploy `dep-dblk4om1egvs73fh5adg`, status `live`.
**Production:** Not in scope. No code or deploy changes.

## Evidence and method
- Firecrawl live scrape (uncached) of both URLs, simulated mobile Chromium via Firecrawl interactive Playwright page session.
- Measured viewport sizes ROVELLC: 320x568, 375x667, 390x844, 430x932, 768x1024. On each: top, middle, bottom scroll, price bar bounding rect and horizontal overflow.
- ROVELLC source readback / page DOM: 1 permanent materials section + 4 remaining details disclosures, 11 material choices, 12 equipment options.
- Ran 5 material selections in actual browser, verified image filename, miniature thumb, selected state, price.
- Ran 12 equipment options in actual browser with group opened; checked selected state, price and inverse selection/undo.
- Checked DAY/NIGHT image, website dark theme (after transition), LV/RU, price details opening and Escape, TXT download browser event.
- MyCabin browser: 320/375/390/430 widths and top/middle/bottom price bar, package choice, final CTA semantics, form presence.
- Only simulated Chromium: NOT_CHECKED on physical iPhone Safari/Android, VoiceOver/TalkBack, reduced-motion, 200% text zoom, actual completed file content and customer submission.
- Scraper screenshot captures requested, but no independent visual image diff/artifact attachment produced in this audit. Do not claim pixel-level visual baseline acceptance.

## ROVELLC measured results
| Width x height | Price fixed and visible top/mid/bottom | Bar height | Horizontal overflow | Mini-preview |
|---|---|---|---|---|
| 320x568 | YES | 89px | NO | hidden because short viewport |
| 375x667 | YES | 94px | NO | visible mid-config |
| 390x844 | YES | 94px | NO | visible mid-config |
| 430x932 | YES | 94px | NO | visible mid-config |
| 768x1024 | YES | 101px | NO | not part of tablet UI |

- At 320px and with all 3 priced options plus an unpriced selection, bar remains visible, buttons do not overlap and horizontal overflow remains absent.
- Base `89 500 €`. Price selection `floor` +2600 => 92100; `curtains` +1800 => 93900; `lights` +950 => 94850; undo resets to base. Unknown-priced selections leave numeric base untouched and show `+ ?`. Reproducible.
- Material context images in 390px interactive test: facade graphite CC2.webp; facade burgundy VV1.webp; floor cherry OO2.webp; walls sand DD1.webp; bath gray RR1.webp. Mini-thumbnail mirrored active image.
- All 12 option toggles: selected `aria-pressed=true`, deselection successful. Three known-price options update total; 9 remaining options are quote-priced, so numerical total intentionally remains unchanged.
- Day/night scene image AA.webp -> BB.webp; site theme toggled separately; RU selected correctly. Price breakdown opens and closes with Escape; TXT download event filename `ROVELLC_S312_Komplektacija_DEMO_ru.txt`. File contents not independently verified.
- Materials always open as a static section; groups 02–05 toggle separately.

## Confirmed or evidence-grounded issues
### P1 — missing meaningful preview on 320x568
Actual preview behavior: `mobile-preview` display none under max-height 629px and width <=600px. On short phone, changing finishes after the hero scrolls away has NO persistent visual feedback. At 390x844 the mini image thumbnail is 87x50px — insufficient for reading fine interior finishes. Product relevance high.
**Recommendation:** attach optional 80–110px collapsible context image above material groups, or an interactive dock/sheet with explicit expand; keep bottom price fixed and avoid >~35% vertical combined overlays. Need prototype test for 320x568 and 375x667 before choosing.

### P2 — image context changes while working in other sections
Observed during open climate/options: the left image / mini view can shift from bathroom RR1.webp to walls DD1.webp due to scroll-intersection synchronization; the user is no longer editing materials. This is not a demonstrated state-loss bug; it is unexpected visual context for equipment choice.
**Recommendation:** activate scroll-linked contextual image only when material group is the primary visible intersection; otherwise freeze last explicitly selected context or show overview. Test layout after opening accordions.

### P2 — tiny guidance and high information density
Actual computed sizes (mobile 390): material labels 12px, material disclaimer 11px, fixed bar eyebrow 9px. Each material group repeats an identical disclaimer, and first group starts with three manufacturer-tech bullet statements before finish cards. Expert heuristic: these de-emphasize task-critical choices and increase reading effort.
**Recommendation:** one summary caveat above material gallery; replace repeated 11px lines with a single clearly worded note; move manufacturer details below the main choices. Favor 13–14px card labels and readable price caption, assess 200% zoom.

### P2 — conversion flow differs from MyCabin
ROVELLC is demonstrational and only downloads TXT (confirmed browser download event); no production quote request workflow. MyCabin has named price including VAT, a summary/action button, share/save, and a contact form to request a quote. This is a scope difference, not an ROVELLC prototype bug.
**Recommendation for production scope only:** post-config quote CTA using saved selection, clear price basis, explicit unknown-cost coverage, and form success/error states; obtain owner and client approval before implementation.

### P3 — bottom CTA hierarchy
ROVELLC price bar’s large primary-looking action is `Lejupielādēt komplektāciju` (download); users seeking a quote could interpret it as the only available next step. Avoid framing it as ordering until working lead form approved.
**Recommendation:** move download to secondary action once quote function is available; keep price as dominant information.

## MyCabin comparative observations (not a blanket quality claim)
- Mobile 390x844: MyCabin floating price bar `position:fixed`, approx 113px high, showing `Kopējā cena (ar PVN)` and `Izvēļu kopsavilkums`.
- MyCabin standard package selection changed €167,875 -> €175,955 and house image to L100-STANDARD.jpg.
- MyCabin includes 3 package tiers, multiple fit-out types, priced individual options, service/installation sections, summary, save/share, form and quote CTA.
- MyCabin fixed bar disappears as user reaches final form (its bounding rect moves below viewport); ROVELLC bar remains pinned even at bottom. Interpret as contextual difference, not a definitive MyCabin bug.
- MyCabin at 320px showed document width 359px vs viewport 320px. Concrete overflow culprit: `.config__meta-item` 'Siltumsūknis' extends to x=359; other tested widths 375/390/430 did not overflow.
- MyCabin initial large mobile hero image area about 375x234px and allows visual choices; ROVELLC offers a 345x230px hero on 390px screen then an 87x50px mini-preview. Neither design can be deemed objectively more usable without task testing; ROVELLC has stronger always-visible price, MyCabin has clearer completion path.
- MyCabin published prices, VAT, packages, offering and services are THEIR data; do not import them into ROVELLC.

## Verdict by scope
- **PASS_SCOPE_ONLY:** Core ROVELLC mobile configurator functions in simulated Chromium; 5 viewport price visibility / no horizontal overflow; 5 sampled contextual material interactions; all 12 equipment toggles and undo; 3 numeric demo supplements; DAY/NIGHT, RU, price breakdown Escape, download event.
- **REWORK:** On very short mobile screens 320x568, users cannot view their selected finishes while editing after hero scrolls off; preview is entirely suppressed. Need product/UI improvement, not broken JavaScript.
- **REVIEW:** Tiny text and repeated caveats; scroll/accordion image context; mobile preview size and clarity.
- **NOT_CHECKED:** physical device/Safari, mobile performance/CLS/LCP and web vitals, actual image-diff visual review, long session persistence across browser restore, 200% zoom, full accessibility audit, full TXT decoded content, lead form backend (does not exist in owner preview), 18-model MVP.

## Proposed acceptance / next owner decision
1. Decide design variant for short-phone preview (compact dock vs expandable thumb) without hiding price.
2. Simplify material intro and repeated captions, retaining honest cost caveat.
3. QA 320x568, 375x667, 390x844, 430x932 and 200% text zoom; visually verify 4 contexts plus night / locale.
4. Confirm whether the next CTA should remain demo TXT or the production quote form is within approved MVP.
5. No code/production modifications until review and explicit approval.
