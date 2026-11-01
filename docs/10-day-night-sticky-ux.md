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


## In-place owner preview release — 2026-11-01

- Owner explicitly authorized updating the existing **single** owner-preview URL, instead of creating any additional test sites or branching more prototypes.
- GitHub PR #6 merged into the branch already linked to the owner-preview: `feature/etf-architectural-atelier-ui-20261101`, merge SHA `c2fdc792f45f2fa1104025caa1c3d27ef6f75dba`.
- Render service: `fibo-etf-atelier-owner-preview` (`srv-dbj7148473hc73bb1k7g`), static site publishing `prototype/`; manual deployment because `autoDeploy=no`.
- New deploy `dep-dbjejtfb9u1s73dqdd00`: final status **live** with merge SHA `c2fdc792f45f2fa1104025caa1c3d27ef6f75dba`.
- Unchanged canonical preview: https://fibo-etf-atelier-owner-preview.onrender.com/
- Published raw HTML fetch: HTTP 200; confirmed `theme-nav`, `quickPrice`, night-theme CSS, photo mappings and asset references are present.
- Independent browser read-only check (LV): main header contains `Diena/Nakts`, initial compact estimate **108 000 €**; switching theme to Night sets page background `rgb(23,27,25)` and anthracite-night.webp; returning Day shows K.webp; estimate unchanged and no browser errors observed in this path. Sticky CSS positions were reported active during desktop scroll.
- Mobile/facade/price extended automation timed out; corresponding responsive and extended interaction criteria remain **NOT_CHECKED**. No claims of a complete mobile or accessibility audit.
- No new Render services or separate review URLs were created; main and client production remain unchanged.
- Next: owner reviews this exact URL and requests direct iterations in the current prototype; verify mobile/edge states as needed.

## Owner-requested UX adjustment — 2026-11-01, in-place

Owner reviewed scrolled desktop screenshot and requested (1) more breathing room above the sticky left image, approximately matching the page side gutter, and (2) move the compact calculation away from the sticky RIGHT configuration panel to the area below the image on the LEFT, adjacent to the selected-configuration pills.

Implemented directly in the existing owner-preview source branch, without a new site or feature branch:
- `prototype/index.html`, commit `648ad75478612d41e31aa7bf10dcfc2bbc767ab4`.
- Desktop sticky left visual top offset changed 16px → 36px; visual height `clamp(310px,48vh,535px)` supports room for quote and selections beneath it.
- `quickPrice` and `quickRequest` relocated into left `.below-card`, under `ВЫБРАННАЯ КОНФИГУРАЦИЯ`. No sticky overlay inside right configuration. Compact quote uses minimal outline CTA and no elevation, including Nightfall theme.
- Reuses original `calc()`, `quickRequest` handler and the bottom detailed total. Original RU/LV localization intact.
- Source validation: one `quickPrice`, left of `<aside class="config">`; one bottom `totalPrice`; JavaScript inline source parsed; both theme styling paths preserved.
- In-place Render deploy `dep-dbjerg5g1s2s73fhu3ng` of the exact HTML commit finished with status `live`; unchanged URL https://fibo-etf-atelier-owner-preview.onrender.com/.
- Fresh external rawHTML fetch HTTP 200 confirmed the new price lives within left markup and the right markup no longer contains price overlay. Screenshot capture succeeded. Extended full interactive desktop/mobile QA did not complete (browser automation timeout) and remains NOT_CHECKED.

Next: owner visual review of same URL, particularly at scrolled desktop position and on narrow laptop screens; adjust directly there if requested.


## Owner approval and final icon-only refinement — 2026-11-01

Owner explicitly approved the current daylight/nightfall prototype layout, texts and price placement. Scope of remaining change: convert textual day/night switches to restrained icons in the existing prototype, not an approval of client deliverables, commercial prices or a production release.

Art direction (Digital Art Director pilot 0.2.2; reading completed from source revision `7288045be692352d008d0168e89617776933b5a9`):
- Brand-specific thesis: minimal, finely outlined architectural **sun / crescent** glyphs with warm-green daylight selection and bronze Nightfall selection, no emoji, gradient decoration or new icon/font dependency. A playful neon/glossy day/night control would conflict with ETF's quiet architectural positioning.
- Applied K02: preserve accessible LV/RU labels in visually hidden text and localized title attributes; retain existing `i18n.js` without a translation reset.
- Applied K03: preserve theme palette and focus rings. Computed contrast for selected foreground/background: daylight white on forest #314338 = 10.55:1; dark #171B19 on bronze #BD9C70 = 6.75:1. This calculation does not establish full WCAG conformance, especially across imagery and focus states.
- Applied K10: one refinement of an approved design; no alternative style proposals or new branches.
- Baseline visual evidence: owner-supplied scrolled RU desktop screenshot of original on-photo text toggle (`image(3).png`), actually viewed. After-deploy screenshot was generated by Firecrawl but could not be retrieved and viewed as pixel bytes; therefore final *artistic pixel QA* is `BLOCKED_VISUAL_QA`, even though interactive functional QA passed.

Implementation:
- `prototype/index.html` committed directly to existing Render-linked branch at SHA `91eb636ec3e6d15aa0c41730dc2ee73a4c335770`; no new branches or preview service.
- Top switch: two icon-only SVG links with `aria-current=page`, keyboard focus and LV/RU visually hidden labels.
- Exterior photo lighting switch: matching icon-only SVG buttons, retaining `aria-pressed`, existing state logic and all three night/day facade pairs.
- Original layout, live price calculation, other copy, original detailed estimate and both visual themes preserved.

Verification:
- Render workspace `tea-dba7n2gm7kps73fq8j30`, service `srv-dbj7148473hc73bb1k7g` confirmed to be the same ETF static owner preview, autoDeploy disabled.
- In-place deploy `dep-dbjev7942hec73cqs4kg`: **live**, exact commit `91eb636ec3e6d15aa0c41730dc2ee73a4c335770`.
- Fresh cache-busted request (`?variant=1&revision=91eb636ec3e6`) HTTP 200 and actual HTML with four SVG mode icons; ordinary URL briefly returned cached old markup after deploy, so force-refresh if needed.
- Read-only Firecrawl browser QA (current live URL): LV accessible labels `Diena/Nakts`, click Night → `data-theme=nightfall`, active moon and `anthracite-night.webp`; click Day → `data-theme=atelier`, active sun and `K.webp`.
- RU language switch verified accessible `День/Ночь`; 390×844 viewport header elements measured without overlaps (logo right edge 182.2 px, mode controls x226–316, language selector x323–355).
- JS syntax, icon counts (2 sun + 2 moon), existing click handlers, current price block placement and image mappings verified in source.
- NOT_CHECKED: independently retrieved and viewed after-screenshot, full mobile scroll, all facade combinations, complete WCAG/performance QA. None of these should be inferred from successful deploy.

Current owner-review URL: https://fibo-etf-atelier-owner-preview.onrender.com/
Status: small UI implementation released to existing owner prototype; user acceptance of this *last icon revision* not yet recorded.
