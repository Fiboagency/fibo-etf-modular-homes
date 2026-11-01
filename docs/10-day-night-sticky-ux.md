# ETF — Day/Night visual theme and persistent price UX

Date: 2026-11-01
Task ID: ETF-UX-20261101-DAY-NIGHT-PRICE
Status: OWNER REVIEW / PREVIEW ONLY

## Owner-approved boundaries
- Use latest owner-approved Architectural Atelier layout and existing RU/LV text as the source of truth; do **not** replace it with the older Russian-only dual-concept branch.
- Provide complete light and dark visual systems, with Day / Night switch in the top navigation.
- Include all owner-uploaded day/night facade photographs, preserving old daytime K.
- Reduce user friction while building a quote: keep image and estimated total in view on desktop.
- Do not change prices/formulas, packages, VAT caveats, or demo request delivery.

## Evidence and source
- Screenshot from owner on 2026-11-01, desktop ~1516 px: photo left, parameter card right; current price located after six lengthy option groups.
- Latest source: `feature/etf-architectural-atelier-ui-20261101/prototype/index.html` and `prototype/i18n.js`.
- Existing approved night visual token reference: `docs/08-dual-theme-implementation.md` (Nightfall: #171B19 base, #242A27 surfaces, #BD9C70 bronze, #F1ECE3 text).
- Existing night photo mapping: `docs/09-night-facades-K-L.md`, previous PR #5.

## Implemented in this feature branch
1. Preserve all existing Atelier heading, supporting copy, choices, product options, and existing RU/LV translation script.
2. Add link-style header switcher: Day (`?variant=1`) and Night (`?variant=2`). Active link has `aria-current=page`. Browser back/forward updates the style. Configuration data remains.
3. Night mode uses approved Nightfall color system; same structure and texts, without older dark hero claims. Switching themes selects the corresponding day/night facade preview.
4. Photo source mapping for each facade:
   - Natural: A.webp / B.webp.
   - Anthracite: K.webp / anthracite-night.webp (new K sourced by blob SHA).
   - Burgundy: J.webp / burgundy-night.webp (new L sourced by blob SHA).
   Interior and bathroom remain independent of facade lighting; only available images are shown.
5. A compact price + demo-request CTA directly under configuration header, updated from the same `calc()` result as the existing final breakdown and request form. Original full breakdown and button stay.
6. Desktop (`min-width:841px`): sticky left preview with a viewport-relative image height, while full document scrolls through options. Mobile: natural document flow and sticky price summary in the card, no fixed overlay blocking selection.
7. New interface wording added to RU/LV translation map. No new locale claims.

## Interaction and acceptance contract

| Scenario | Expected outcome | Status |
| --- | --- | --- |
| Direct open `?variant=1` / no query | Approved daylight typography/copy, day exterior | Code implemented; browser NOT_CHECKED |
| Direct open `?variant=2` | Same approved content, Nightfall palette and matching night exterior | Code implemented; browser NOT_CHECKED |
| Switch theme then press Back | Active theme and associated facade photo restored without losing size/floor/options | Code implemented; browser NOT_CHECKED |
| Select all facade colors, use local Day/Night control | All six source photo pairs resolve without disabling night | Asset paths checked; rendered QA NOT_CHECKED |
| Change model/finishes/options | Sticky displayed estimate equals existing bottom total, request and export | Same `calc()` expression; interactive QA NOT_CHECKED |
| Scroll through all six groups on desktop | Left image stays visible; quote bar remains at top of right card | CSS implemented; visual QA NOT_CHECKED |
| Mobile viewport / text zoom | No horizontal scrolling, no covered controls, focus visible | NOT_CHECKED |
| RU / LV language toggle | No loss of choices; navigation, summary, dynamic nights localized | Translation map extended; browser NOT_CHECKED |
| Keyboard buttons, tab arrows, dialog, reset and failed validation | Existing behavior retained, newly added top CTA opens existing dialog | NOT_CHECKED |

## Known constraints and next steps
- Prototype only; estimated figures fictional; no final prices, VAT policy or SIA ETF commercial offer.
- All five client locales LV/EN/LT/ET/RU, admin, backend, real lead sending, and catalog of >=6 real models remain outside this task.
- Rights for commercial publishing of uploaded renders not confirmed.
- Full WCAG 2.2 review, real screenshot/interaction QA and Render preview verification are pending.
- Do not merge into main or release to client/production without owner approval.
- Next: run an independent desktop/mobile interaction suite on a dedicated preview, confirm the visual rhythm and price behavior with owner, then document acceptance and decide on preview merge.

## Decision log
- SELECTED: preserve the current light copy/layout instead of merging the older dual concept HTML, which would have overwritten LV text and localization.
- SELECTED: sticky in-flow price rather than a fixed overlay, to reduce occlusion.
- OWNER APPROVAL PENDING: this new revision, final sticky placement, and night visual treatment.
