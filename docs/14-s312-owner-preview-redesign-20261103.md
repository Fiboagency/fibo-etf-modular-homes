# ROVELLC S312 — owner-preview redesign (2026-11-03)

## Scope and source
- **One model only:** S312 from ROVELLC Group Catalogue 2026 LV, pp. 19–22. No other models or series added.
- **Owner assets already in feature branch:** `prototype/assets/brand/logo.svg` (ROVELLC logo), two new 1376 × 768 px image files for S312 (day and blue-hour), and existing Fibo footer mark.
- **Verified against the PDF images** (rendered for this review): S312 covered area **38 m²**, **11.5 × 3.3 × 3.35 m**, **approx. 10.5 t**, one bedroom, one living room, one bathroom, one balcony. The catalogue lists **3–5 persons** on p. 20. p. 21 shows the floor plan; p. 22 shows real model/interior photographs.
- p. 16–17 illustrate general manufacturing materials, lighting, sanitary equipment and **electric curtain**, but do not provide a model-specific price list or whether each item is included with S312.
- **Seller email** explicitly mentions heated floors and electric curtains as examples of price-changing extras.

## Changes to the earlier Architectural Atelier prototype
- Replace invented 60/80/100 m² options and unrelated Scandinavian house photos with one genuine **ROVELLC S312** product story.
- Replace header with provided `logo.svg`; keep Fibo Agency credit discreetly in footer.
- Show real S312 dimensions and a verified catalogue-based room summary.
- Day/evening switch uses **the two new uploaded S-series illustrations** (do not create artificially darker image: existing blue-hour scene reads clearly).
- 3 example toggles: electric curtains **+1,800 €**, heated floor **+2,600 €**, extra LED lighting **+950 €**.
- Base **89,500 €**, *arbitrary DEMO value*. No customer-facing claim that ROVELLC or ETF sell S312 at this amount. No known VAT, shipping or installation included.
- Constant viewport-bottom price panel on mobile and desktop; responsive layouts 1440 / 390 targeted; safe-area bottom padding.
- LV first-load, RU selector; switches preserve options. State stored locally; name/email never persisted.
- Demo request still downloads local TXT; **no data submitted to a server**, no actual order, no backend, no production deployment.

## Real use limitations
- Client and owner may use the new logo/photos for presentation according to their instruction. **Public production-use permission is not independently documented**; do not assume broader licensing beyond the owner's claim.
- The photos show the same S-series facade; choosing interior equipment updates *the price and line item*, not pixels of the exterior because no variant images were supplied. Do not pretend those variants are rendered.
- p. 20–21 layout is supplemented with a **custom schematic SVG** (`prototype/assets/s312-layout-schematic.svg`), not an engineering/factory drawing; it is available in an expandable section.
- Only one landing/configurator prototype; the planned 18-model catalogue, admin panel, CRM and production forms remain out of scope.

## QA evidence
- Source on feature branch: `prototype/index.html`. Created without external application dependencies.
- Read-back of GitHub content: 24,232 characters, UTF-8, LV/RU keys present, no missing translation keys in static check, three option controls, fixed-bottom price CSS, `noindex,follow`, and two referenced source images.
- Actual supplied day/evening image bytes displayed and inspected in the research browser; both loaded at natural size 1376×768.
- **Actual browser visual review completed** through a public GitHub-branch HTML preview (`https://htmlpreview.github.io/?https://github.com/Fiboagency/fibo-etf-modular-homes/blob/feature/rovellc-s312-owner-preview-20261103/prototype/index.html`). Viewed desktop **1440×900** and mobile **390×844** (also checked narrow **320×720**). This is not a Render deployment or independent cross-browser QA.
- Desktop preview: ROVELLC SVG logo and day/evening PNGs loaded, photo view focal area visible, panel and fixed price aligned.
- Mobile preview: no horizontal overflow (`documentElement.scrollWidth` 375 with viewport 390; 305 with viewport 320), price band `position: fixed`, remains visible after scrolling down the settings. Image and switches visible at top.
- Functional browser checks: 89,500 € initially; electric curtains selected -> **91,300 €**; all 3 options selected -> **94,850 €**; switching to evening toggles the image; LV→RU changes copy while retaining price; expanded floor-plan image loaded correctly after scrolling; configuration, RU locale, and evening mode survived reload; modal opened/closed. A local download was attempted but the remote browser interpreter failed, so actual saved TXT content is **NOT_CHECKED**.
- Remaining before customer presentation: check actual TXT downloads/contents (browser download check not completed), deep keyboard/focus/tab-order and contrast measurements, real iOS Safari and Android Chrome device rendering, and independent PR-head acceptance screenshots; verify the deployed Render service matches the reviewed commit after owner approval. No performance or WCAG claim.

## Release
- This code is isolated to `feature/rovellc-s312-owner-preview-20261103`. No merge to original branch, no changes to `main`, existing Render preview or customer website.
- **Design concept and deploy require owner approval** after genuine screenshots and QA; PR remains DRAFT.
