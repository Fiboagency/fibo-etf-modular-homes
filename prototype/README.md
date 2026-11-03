# ROVELLC S312 — Fibo Agency owner-preview (static DEMO)

**Status:** Owner-approved content/UX scope (20/20 editorial decisions), implemented in an **isolated review branch**; NOT merged or deployed. Do not treat this as real ETF production or a quotation.

**Preview baseline:** https://fibo-etf-atelier-owner-preview.onrender.com/  
**Review branch:** `feature/s312-approved-content-ux-20decisions-20261103`  
**Render publish directory:** `prototype/` (auto-deploy OFF).  
**Primary implementation:** `index.html`; existing AA/BB photos, layout SVG, brand marks and Onest fonts are reused.

## Current scope

- Exactly one house: ROVELLC S312. No 18-model catalogue, finish selector, guessed sizes or variants.
- Architecture-first presentation (*The Destination / Quiet Architecture*) for private customers **and** hospitality/glamping operators.
- LV by default and RU as alternate locale; both also used for generated TXT.
- Manufacturer/catalogue-based facts: **38 m² covered area** (not certified living area), **11.5 × 3.3 m** nominal dimensions, bedroom/living/bathroom/balcony. Known disagreements on height, occupancy, BOM and local compliance remain in the disclosure.
- Five collapsible equipment groups, one open at a time. Selected options persist across navigation and locale/theme changes.
- Fixed DEMO price: `89 500 €` base, `+2 600 €` heated floor, `+1 800 €` electric curtains, `+950 €` additional LED. Other listed options selectable as **Price on request** and excluded from the numeric subtotal.
- Single **Download configuration** action; a locally generated UTF-8 TXT includes model/facts, chosen options, demo sum and the caution. **No contact form, email, backend, CRM, or data submission.**
- Independent site DAY/NIGHT theme and S312 photo DAY/NIGHT; animated transition, reduced-motion fallback.
- Mobile compact pinned preview when the configurator is in view, suppressed on short viewports; fixed price bar with expandable cost breakdown.
- `noindex,follow`; SEO and marketing production release are separate stages.

## Source and open questions

Review manufacturer discrepancies and unresolved statements in:
- `../docs/18-s312-technical-dossier-and-conflicts-20261103.md`
- `../data/s312-source-data-20261103.json`
- `../docs/25-s312-day-night-preview-deployed-20261103.md`

No actual production prices, VAT basis, delivery, installation, engineering guarantee, local regulatory eligibility or image commercial licensing are asserted by the prototype.

The earlier art-review page `design-review.html` was removed from the public publish directory with owner approval. Its history remains in Git and art-direction documents, e.g. `../docs/06-premium-brand-art-direction-ru.md`.

## Review / QA

Open `index.html` with a local static server from the `prototype/` folder, or use a browser sandbox to render the GitHub branch HTML against existing preview assets (not equivalent to a deploy). Compare widths 320 / 390 / 768 / 1024 / 1440 and LV/RU × theme DAY/NIGHT × house photo DAY/NIGHT. Check config persistence, one-open accordion, price math, unknown-price exclusions, TXT contents, fixed preview clearance, keyboard focus, reduced motion, contrast, zoom and touch devices.

**Release gate:** draft PR and documented checks for owner review. Do not merge or trigger Render deploy without separate explicit owner permission.
