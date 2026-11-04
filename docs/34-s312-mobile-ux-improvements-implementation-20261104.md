# ROVELLC S312 — mobile UX improvements implementation and QA

**Task:** UX-S312-MOBILE-REWORK-20261104
**Date:** 2026-11-04 (Europe/Riga)
**State:** `IMPLEMENTED_IN_BRANCH / NOT_MERGED / NOT_DEPLOYED`
**Base:** `feature/etf-architectural-atelier-ui-20261101` after merged audit PR #42, commit `63d3c7d980678d3a04751219d68cca8e9d926cba`.
**Audit source:** `docs/33-s312-mobile-ux-audit-vs-mycabin-20261104.md`.
**Environment:** existing owner-preview URL https://fibo-etf-atelier-owner-preview.onrender.com/ (this PR is **not yet** published there).

## Owner authorization and boundary
Owner approved proceeding with implementation after the mobile audit ("обьеденил. можешь реализовывать"). This branch addresses the design/interaction improvements only, not new commercial scope.
No quote-request form, CRM integration, external delivery, new product prices, five-language expansion, `main`, Render deployment or production changes.

## Implemented improvements

### P1 — Mobile image feedback on short devices
- Removed the CSS rule that hid the mobile preview at heights <=629px.
- Compact fixed top preview now operates within material selection on 320x568 as well as other supported phones, as long as the main hero is out of view.
- Preview shows an enlarged 92–112px wide thumbnail with current facade/interior, plus an explicit, keyboard-usable expand/collapse button.
- Expanded view uses a larger image; the separate «View full house photo» button returns to the main image.
- DAY/NIGHT scene buttons remain available only while viewing a facade, as before.
- Mobile preview auto-collapses/hides when the materials gallery is no longer in the reading area. It does not cover the entire site or remain fixed over the equipment sections.
- Retains fixed bottom cost/action bar without sharing its scroll state or interactivity.

### P2 — Scroll photo limited to material context
- `detectActiveFinish()` now applies scroll-linked image changes only when the material gallery intersects the central reading line.
- Outside materials, changing/opening climate, controls, furniture and engineering options does **not** replace the previously selected preview image.
- Explicit material choices still update the image and miniature immediately, preserving existing facade day/night logic.

### P2 — Material information hierarchy and legibility
- Single upfront localized caveat about visualizations and unpriced nonstandard materials.
- Manufacturer/catalogue technical statements moved below the samples to an accessible native collapsible `details` block. Not deleted.
- Removed four repeated 11px caveats from each material group.
- Material sample labels 13px (up from 12px), section headings 15px on mobile, price caption 10px on typical mobile and 9px on <=350px to protect 320px layout.
- LV and RU strings added for new elements, including expansion controls.

## Protected behavior
- Same S312 and 11 material choices, 12 equipment options and 3 priced DEMO supplements.
- DEMO amount, + ? unpriced indicator, save/download TXT, stage DAY/NIGHT and site day/night, keyboard arrow navigation in material radios, language selection and four nonmaterial accordions.
- No image assets were altered.
- Quote button/backoffice/CRM not added: requires separate MVP/data authorization.

## Browser-based test evidence (pre-merge candidate)
**Method:** GitHub source for this feature branch injected into an isolated, real browser session on the public owner-preview origin using Playwright via Firecrawl. The live published URL was not modified; only session DOM was replaced for candidate validation. Styles were layered from branch CSS. Browser-simulated responsive QA, NOT physical-device verification.

**Initial load:** 11 finish choices, 12 equipment choices, 1 shared material price note, no `pageerror` reported.

| Viewport | Compact preview visible while editing materials | Expanded preview works | Hidden on equipment | Fixed price | Horizontal overflow |
|---|---|---|---|---|---|
| 320 × 568 | PASS | PASS (225px expanded) | PASS | PASS | NONE |
| 375 × 667 | PASS | PASS (251px expanded) | PASS | PASS | NONE |
| 390 × 844 | PASS | PASS (272px expanded) | PASS | PASS | NONE |
| 430 × 932 | PASS | PASS (272px expanded) | PASS | PASS | NONE |
| 768 × 1024 | Desktop/tablet, no compact preview | Not applicable | Not applicable | PASS | NONE |

- Mobile compact dock stays around 76–80px high, expandable on demand; bottom fixed bar stayed pinned in tested scenarios. The expanded dock may occupy substantial space on very short screens, so owner visual review is important.
- Graphite facade click: checked true and `CC2.webp` photo; night scene changed to `CC1.webp`.
- Dark theme separately switched to `night`.
- Grey marble bathroom choice yielded `RR1.webp`; opening climate and toggling warm floor twice retained `RR1.webp` during equipment interaction, as intended; price returned to base `89 500 €`.
- RU version of shared material note and manufacturer-spec heading rendered as translated; LV initial note present.
- Price breakdown `aria-expanded=true` and Escape to `false` passed.
- CSS brace balance, preserved 11 swatches, 12 equipment data, first fixed materials group and 4 other accordions checked from source; source readback will be confirmed during PR validation.

## Remaining tests and acceptance gates
- Owner visual review on real iPhone Safari + Android Chrome, especially 320×568 and safe-area notches.
- Reduced-motion transitions, keyboard focus when expanded preview auto-collapses, 200% text zoom and VoiceOver/TalkBack.
- Confirm real-device smoothness and image loading; no CLS/LCP performance measurement captured.
- Independent screenshot baseline review across compact/expanded DAY/NIGHT in both LV/RU.
- Real customer quote workflow, 18-model data and five languages remain a separate approved MVP phase, not included in this demo UX patch.
- No automatic merge or Render deployment: PR review and owner release decision required.

**Status:** `IMPLEMENTED` and `PASS_SCOPE_ONLY` for simulated browser interactions; independent physical-device/visual QA `NOT_CHECKED`.
