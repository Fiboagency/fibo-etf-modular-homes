# ROVELLC S312 — order-first configurator layout (2026-11-04)

**Status:** code complete in isolated feature branch; **not merged or deployed**. Owner review and rendered QA required.

## User request and observed defect

Source: owner-provided desktop Chrome recording, 27.4 seconds, 2240×1440. Do not publish source recording in this public repository.

The video shows that the existing left column's fixed/sticky hero and the subsequent architectural visual rail can overlap while scrolling; the house-image view is repeatedly displaced and another image appears in the same region. Root cause in source: `#house { position:sticky; top:96px }` inside a tall left column still containing `.visual-rail` and ancillary editorial elements.

The owner requests a simpler, MyCabin-like **order/configuration page** — not a new editorial homepage. Do not remove or rewrite existing equipment/material/price logic.

## Implemented scope

1. Remove the visible oversized two-part `.hero-heading` (headline and side description) from the configurator page. Preserve the header/logo, DAY/NIGHT theme and LV/RU controls. Add a screen-reader-only H1 using the existing title translation.
2. Place `.main-layout` immediately below header with a small top gap.
3. Desktop left column contains **one** photographic `#house` stage (facade/interior context, day/night when applicable), a compact materials/equipment selection summary, and the existing price/download actions under the image.
4. Make the *whole small left visual column* sticky; restore `#house` to nonsticky position. Avoid duplicate visual rails or nested competing sticky blocks.
5. Move the entire original support content — photo disclaimer, S312 facts, plan details, source/conflict details and `.visual-rail` with its image/copy — **unchanged in content** to a block **after the configurator**. Keep the existing project-path editorial section after this moved block, to let the owner decide later what to retain.
6. Reuse the original cost bar and price details DOM/IDs for desktop in the left column; on mobile and tablet it retains the existing bottom-fixed behavior, not a second price.
7. Preserve the compact mobile top preview and the overall mobile one-column workflow; support content now appears after the configurator rather than before it.
8. Preserve 11 added material swatches, 12 original equipment options, price calculations, unknown-price handling, local storage, LV/RU, DAY/NIGHT and TXT export.
9. Avoid resetting the displayed image to facade when no material group intersects the scroll sampling line; retain the last relevant image rather than flicker back on every gap.
10. Place order-layout style overrides **after** `future-living.css`, so the approved theme styles do not undo sticky/price/mobile changes.

## Acceptance criteria

- At 1440×900 and 1280×720: only one image on the left, no overlap/jump during slow/fast scroll, selection controls remain usable on the right, price/selected materials under the image. Background scroll continues normally, no separate nested scroll.
- At 390×844, 375×667 and 320×568: original compact top mini-preview and bottom-fixed demo price remain, no overlap with controls; no horizontal scroll.
- Expanded material swatches switch image immediately. Scroll through facade/floor/walls/bath changes contexts without flashing to facade in gaps. DAY/NIGHT facade retains state, night mode works.
- Any prior selected equipment, DEMO pricing, local storage and download text remain identical in behavior. Unpriced finish variations still require quotation.
- Detailed info/facts/plan/gallery appear **once** and only below the configurator. The initial screen contains logo/header plus the image and configuration, without a large architectural headline.
- Test tab focus, aria labels, price-details close via Escape, reduced-motion behavior and asset image loads.
- No deploy to client production, no autoDeploy setting changes, no client emails.

## Verification completed at PR creation

- Modified JS syntax compiled: PASS.
- HTML tag open/close counts on major structural elements: PASS.
- 12 original equipment IDs still present: PASS.
- Price, price-details, images, mini-preview and finish-control IDs remain unique: PASS.
- Hero removed, post-config content relocated, new CSS last in cascade: PASS.

## Pending

Live rendered cross-device QA on the review branch, including focus/keyboard checks. Deploy only once PR is approved/merged by the owner, using existing Render service `fibo-etf-atelier-owner-preview` (autoDeploy is off).
