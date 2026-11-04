# ETF — pre-client mobile QA and release checklist

Date: 2026-11-01. Target: preview-only [ETF Atelier](https://fibo-etf-atelier-owner-preview.onrender.com/).
Task: issue #7. Source branch: `fix/etf-preclient-mobile-qa-20261101`. Target preview branch: `feature/etf-architectural-atelier-ui-20261101`.

## Owner's approved branding boundary
The header has the original `ETF. / MODULAR HOMES` wordmark with day/night and LV/RU controls only. **Do not reintroduce Fibo Agency icon/logo/link into the header.** Preserve the existing Fibo Agency footer logo/wordmark and its attribution text (no 'free' language).

## Live evidence before patch
- Render static service `srv-dbj7148473hc73bb1k7g`; last observed live commit `e57aaf332537a0e5a68cc9f6b28c02858770fbcd`. Repo tip `abfcd1fd23444a5c243b3000a1b6ec78e9688eef` contained later documentation only.
- **Fresh re-test after owner header restoration**: 320 px viewport document clientWidth/scrollWidth both 305 px. Previous header overflow was already fixed by the owner's latest change. No redundant header changes.
- Earlier QA showed a 320 px request dialog overflow +36 px, 340 px +16 px, and bathroom breakdown monetary value wrapping.
- Initial live QA verified source images for all 12 combinations, prices/update logic, translations LV/RU, day/night switching and reset.

## Patch
1. Narrow-modal fields: `min-width:0` for form/grid children and `width:100%;max-width:100%` for inputs, 320 px-safe modal padding.
2. Price breakdown: flex-wrap the left description but preserve the whole monetary value on one line; slightly larger mobile type.
3. Improve modal title/close layout at narrow widths and increase close target to 36 px.
4. Add explicit `role="group"` to three noninteractive elements already carrying `aria-label`, following axe incomplete ARIA findings.
5. No product, image, marketing, translated text, pricing algorithm or branding changes.

## Release acceptance
- Header width 320, 340, 360, 375, 390, 430: no horizontal overflow; original ETF-only branding preserved.
- Request modal at same widths: no internal horizontal overflow, fields fully visible, submit reachable via vertical scroll; dark/light display.
- Breakdown monetary values never split between digits and euro sign.
- UI: both variants switch, image mappings work, all prices and selected options are unchanged across LV/RU theme switches and reset.
- Footer Fibo Agency logo is visible, title unchanged, no 'free' attribution.
- No unhandled console errors, downloaded requests remain local demo only, no server-side data submission.
- Actual Render deploy must report `live` and a new-browser verification must pass before owner/client shares the link.

## Non-goals
Production release, `main` branch, paid transactions, customer contact or quote submission, real prices, 5 production languages, full accessibility certification or mobile device lab.

## Status
Source patch implemented in separate branch. Preview deployment and final live regression **pending**; update outcome and status after independent verification.
