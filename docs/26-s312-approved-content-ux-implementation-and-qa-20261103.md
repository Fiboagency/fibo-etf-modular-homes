# ROVELLC S312 — implementation and QA handoff for 20/20 owner-approved decisions

**Date:** 2026-11-03 (Europe/Riga)  
**State:** isolated GitHub Draft PR candidate, **NOT MERGED / NOT DEPLOYED**  
**Source branch:** `feature/etf-architectural-atelier-ui-20261101` at `8219ec367c00b05528c1d78a37eebfc85d3209a8`  
**Implementation branch:** `feature/s312-approved-content-ux-20decisions-20261103`  
**Render service:** `srv-dbj7148473hc73bb1k7g` / publish folder `prototype` / autoDeploy **off**  
**Existing live baseline (unchanged):** https://fibo-etf-atelier-owner-preview.onrender.com/

## Delivered

### Editorial / information architecture
- Dual B2B + B2C positioning in hero and single three-part storytelling section: place, comfort, implementation.
- Preserved Quiet Architecture, current Onest typography, existing AA/BB assets and site-theme animation.
- One compact product fact card (covered 38 m²; nominal 11.5×3.3 m; rooms and balcony), a collapsible plan and separate supplier technical evidence. No guessed height/occupancy.
- Removed duplicated near-image selection summary, redundant late story, and single-model accordion; remaining equipment categories renumbered 01–05.
- One consolidated DEMO disclosure below configuration; short DEMO label remains by fixed price. Removed repeated technical notes from equipment buttons.
- Updated README references, removed obsolete `prototype/design-review.html` from published static folder. Source history remains in Git.
- LV/RU only, LV initial default when no stored preference; preserved robots `noindex,follow`.

### Interaction
- At most one equipment accordion group open; selected options preserved across group, locale, theme and photo scene changes.
- Price breakdown within the configurator and fixed price bar; opening details from price or `Sastāvs/Состав`, accessible close/Escape/focus restoration.
- Single action `Lejupielādēt komplektāciju/Скачать комплектацию`; removed name/email form and dialog entirely. TXT is generated locally as UTF-8 BOM text with facts, chosen priced/unpriced equipment, subtotal and disclaimer. No POST/CRM/email.
- Preserved baseline 89 500 € + DEMO equipment 2 600 / 1 800 / 950 €, excluding all other selected unknown-price items from subtotal; `+ ?` reflects unpriced selections.
- Two independent site DAY/NIGHT and S312 AA/BB photo DAY/NIGHT controls, including mobile mini preview and existing theme transition.
- Compact mobile fixed preview appears while configuring (not while hero visible), hides on short visual viewports and is re-evaluated on resize/visualViewport resize. Fixed price stays at bottom.
- Screen reader labels for interactive controls localized, existing live selection announcements and focus restoration retained.

## Actual tests performed

**Method:** Opened the real Render owner-preview origin in an isolated Firecrawl Chromium browser session, fetched the exact HTML of the **unmerged GitHub review branch** over HTTPS and injected it into the browser DOM with `page.set_content`. Relative image/font assets resolved against the already live origin. This is a real browser integration test of candidate HTML and live assets, **not a deploy**.

| Check | Result |
|---|---|
| HTML served from GitHub and S312 hero | PASS: HTTP 200; live AA image loaded (natural width 1678 px) |
| Five equipment groups, one initially open | PASS |
| 320 / 390 / 768 / 1024 / 1440 px | PASS: no horizontal overflow (scrollWidth ≤ viewport width) and download CTA within viewport |
| All 4 site DAY/NIGHT × house photo DAY/NIGHT combinations | PASS: theme and photo states independent |
| Baseline arithmetic | PASS: 89 500 € |
| Floor heating +2 600 € | PASS: 92 100 € |
| Electric curtains +1 800 € | PASS: 93 900 € |
| Additional LED +950 € | PASS: 94 850 € |
| Unknown-price kitchen module | PASS: numeric subtotal stays 94 850 € and `+ ?` appears |
| Accordion interaction / retaining choices | PASS: opening another group closes prior; selection retained |
| LV → RU localization after selecting equipment | PASS: hero text, CTA and common disclaimer change; amount retained |
| Mobile preview at 390×844 | PASS: visible above configuration, top 8 px / bottom 76 px; price bar top 761 px, no overlap |
| Mobile preview at 390×580 | PASS: hidden |
| Mini DAY control | PASS: changes original scene state and corresponding thumbnail |
| Price breakdown keyboard escape and focus | PASS: details opens, Close focused, Escape closes and focus returns to price trigger |
| Option focus after rerender | PASS |
| JS page errors | None observed in exercised scenarios |
| Form removal | PASS: no name/email form and one download CTA |
| Local TXT generation | Source validated; browser download event observed but sandboxed download artifact was canceled, so **actual downloaded file bytes are not certified** |

**Static source checks:** 15/15 PASS, including JavaScript compilation, noindex, single disclaimer, all relevant DOM IDs, arithmetic constants, locale dictionary, mobile preview and removal of contact inputs.

## Pending / not certified

- Independent real-device iPhone Safari and Android browser QA (safe areas, short keyboard viewports, touch and scroll).
- Full WCAG 2.2 AA review including physical keyboard-only flows, VoiceOver/TalkBack and automated contrast measurements. Existing code has focus/ARIA hooks, but no certified WCAG result is asserted.
- Local TXT download and UTF-8 file opened on actual iOS/Android/desktop browsers; sandbox denied artifact read.
- Real manufacturer/ETF approval of equipment BOM, actual prices, VAT, product measurements, local law/installation feasibility, commercial photo rights, and production contact workflow: **out of this DEMO PR**.

## Acceptance and release gates

1. Owner reviews the branch diff and Draft PR (especially mobile 320/390, dark/light, both photo scenes and TXT).
2. Address any substantive owner changes in this isolated branch.
3. Perform remaining real-device and accessibility checks before claiming full QA.
4. **Do not merge this PR** and **do not trigger Render deploy** without explicit separate permission from the owner.
5. `main`, production, real order handling, CRM and other models are untouched.
