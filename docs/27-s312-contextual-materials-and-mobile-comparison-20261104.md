# S312 — contextual materials / mobile comparison (2026-11-04)

Status: **merged** via PR #33 on 2026-11-04 09:48 UTC; manually **deployed** to existing Render static preview `fibo-etf-atelier-owner-preview` on 2026-11-04 09:59:52 UTC. Render deploy `dep-dblg43c9v7es739udtl0` is `live`, commit `ffda27df1e44debce0084e3a04fe4a3a3547c2b3`. Publication URL: https://fibo-etf-atelier-owner-preview.onrender.com/. **Not a production release.** Interactive cross-device QA and owner review remain open.

## Decision: preserve approved ROVELLC mobile design

Observed at approximately 390 × 844 mobile viewport:
- MyCabin Living 100: fixed/sticky upper house preview area ~284 px, bottom price bar ~113 px. The image is highly visible but vertical configuration area is smaller.
- Published ROVELLC S312: compact 68 px fixed top preview when configurator is in view, ~94 px fixed bottom price bar. The full-size main image is above the options.
- **Decision:** retain ROVELLC's existing mobile layout, its fixed price bar, current compact preview dimensions, and scene controls. Update preview thumbnail contextually to show the material currently being configured. The thumbnail remains clickable to return to the full-size house image.

Reference: https://www.mycabin.lv/konfigurators?model=living-100&market=LV
Source: published ROVELLC S312 owner preview at https://fibo-etf-atelier-owner-preview.onrender.com/

## Additive controls only — original 12 option definitions unchanged

The existing configurator option groups and prices remain intact. New swatches are inserted within the existing **Construction and interior** accordion:
1. Facade: light (AA.webp day / BB.webp night / AA3.webp sample), graphite (CC2 day / CC1 night / CC3 sample), burgundy (VV1 day / VV2 night / VV3 sample).
2. Flooring: light oak (UU1 room / UU2 sample), cherry wood (OO2 room / OO1 sample), dark-grey wood (PP1 room / PP2 sample).
3. Interior walls: light (GG1 room / GG2 sample), warm sand (DD1 room / DD2 sample), burgundy (FF1 room / FF2 sample).
4. Bathroom tile: light marble (TT1 room / TT2 sample), grey marble (RR1 room / RR2 sample).

Image choices are **independent**: floor images intentionally do not expose wall finishes, and wall images intentionally do not expose floor finishes. Do not synthesize or imply a combined realistic render. For all non-facade previews, day/night scene controls are temporarily hidden, and the previous day/night selection is retained for the facade.

## Behavior contract

- Desktop: keep the main left house preview sticky while the existing right-side configuration scrolls; automatically select the matching image for the material section near the viewport reading line.
- Mobile: keep the current compact fixed top preview and fixed price bar; change only the thumbnail image with active material section. No large permanent sticky MyCabin image.
- Tap/click or keyboard arrow interaction on a swatch changes the material, the current large image, and the mini thumbnail.
- Leaving a finish section restores facade preview. Returning to facade preserves the chosen day/night setting.
- Persist new materials separately from the original equipment checkboxes. Existing saved equipment selections are still read.
- Include selected finish values in downloaded TXT summary.
- Pricing: only the existing **DEMO** prices are calculated. Non-default material changes have **unconfirmed** price and are flagged for quotation; do not invent real material surcharges.

## QA and open issues

Static checks completed:
- JavaScript syntax compilation: PASS.
- All 25 referenced image files exist in the feature branch: PASS.
- Existing 12 equipment option identifiers unchanged: PASS.
- Mobile CSS dimensions, theme animation, day/night controls and price bar source preserved: PASS.
- Download summary includes material selections in source code: PASS.

Post-deployment checks still outstanding (published preview):
- Desktop sticky image with expanded accordions and different viewport heights.
- Actual scroll-to-image synchronization, lazy loads and transitions for every finish.
- Mobile 320 / 375 / 390 px, 667 / 844 px height, keyboard/focus interaction, fixed-price-bar overlap.
- Language switches LV/RU, persisted selections, TXT export contents.
- Reduced motion and image load fallback.

## Publication verification

- Render connected to `feature/etf-architectural-atelier-ui-20261101`, repo `Fiboagency/fibo-etf-modular-homes`, static publish path `prototype`, autoDeploy `no`.
- Manually triggered deploy of merged PR #33. Exact commit confirmed by Render API, terminal status `live`.
- Public URL returned HTTP 200; Firecrawl fetched actual published HTML, confirming `#finishOptions`, `const finishes`, all four finish definitions, 11 material samples, original option IDs, bottom price bar and day/night controls.
- Initial live browser inspection confirmed that a floor-selection context updates the left house-image accessible description to the floor material.
- Render error-log query was temporarily unavailable (503 from log backend); no absence-of-errors claim is made.

**Next tasks:** interactive mobile and desktop QA across small viewports, verify scroll synchronization, all scene and swatch selections, visible image loads, persistence in LV/RU, correct TXT export and surcharge labeling; fix defects through separate PR if found. Keep the current published prototype link and do not enable automatic deploy without owner approval.

