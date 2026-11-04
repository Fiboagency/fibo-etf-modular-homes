# ROVELLC S312 — approved visual direction A / Soft-Tech Product Gallery

**Owner selection:** 2026-11-03, in project conversation: “A — Soft-Tech Product Gallery — утверждаю”.  
**Implementation scope:** a nonproduction, isolated proposal applied to the existing S312 owner-preview branch only. **No merge/deploy approval is implied by design approval.**

## Intent and reference

- Main direction: calm premium **product gallery** rather than an architectural consultancy site; inspired by Oura's *clarity and restraint*, not copied from its layouts, assets, trademarks or licensed fonts.
- Source of concept: `ROVELLC_S312_Future_Living_Design_Concept.html` (A visual selection) and `ROVELLC_S312_New_Brand_Art_Direction.md` from the owner discussion.
- Before page: `https://fibo-etf-atelier-owner-preview.onrender.com/`.
- Before deployed commit (confirmed from Render): `30bd007b56453c0b0ded9477c98146a9d471ce14`, deployment `dep-dbktc7ajnfac739tiedg`.
- Two reference browser CSS study screenshots (03 Nov 2026): desktop 1440×900 `e5543eca1c9f8db052ad0dddc4a270f22d017f5547142140b829f83433d854ab`, mobile 390×844 `2861a5bf9a62d09bcc332ff38586212c79b78da610118a59eeaea60ca22eb853` (SHA256; original capture bytes not bundled).

## Design implementation

- `prototype/future-living.css`: isolated style overrides, after existing inline CSS. All CSS `@font-face` declarations remain self-hosted Onest, without new font dependencies.
- Day: near-white `#F7F7F5`, white cards, dark `#222930` type, bright blue `#2869E8` action.
- Night: slate `#141A24`, pale blue actions `#91B7FF`, light text; **this is the A direction's complementary theme, not an implementation of concept B**.
- Product photography larger and rounded, with AA.webp/BB.webp retained.
- Configuration sections: separated rounded controls with clear active selection; no changes to calculations or data.
- Fixed cost bar: brighter surface, blue CTA, DEMO qualification preserved.
- Mobile: one-column structure; photo precedes configuration; two-up facts; permanently visible demo-cost bar.
- Existing content, footer attribution, accessible label structure, SVG logos and all images unchanged.

## Protected behavior and data

- **Only one S312**; no speculative 18-model catalogue and no new materials/options.
- **89 500 €** base demonstration figure unchanged; unknown-price choices still show `+ ?` and do not enter the computed subtotal.
- Site-wide theme switch (animated with `prefers-reduced-motion`) stays **independent** from AA/BB day/night image selection.
- Actual options, existing tally, responsive helper, local `.txt` download, local-only DEMO modal remain.
- Published LV/RU supported; no unapproved EN feature.
- Manufacturer caveats, taxes, shipping and installation disclaimers retained.
- No changes to forms' transport logic, SEO or backend.

## Evidence and checks — prototype style applied to baseline page

**Method:** Firecrawl interactive browser loaded the existing live baseline and injected the exact `prototype/future-living.css` bytes fetched via GitHub raw branch HTTP 200 (11,440 characters). This is a CSS-parity preview, **not** an independent after-deployment screenshot from the new branch.

- desktop LV/day 1440×900 screenshot SHA256: `7c9b70aeba887cfb2213c4471dfd9d2b57104bd5d251b0ec98028a3b26eaf566`.
- mobile LV/day 390×844 screenshot SHA256: `51dcfc26679c017f40a25b408603797ae599b49e2dfb8e75e852e4cc4580b8f3`.
- mobile RU/night 390×844 screenshot SHA256: `e48f27f291e2a1fa0f4bc59de0a0de54be3bb36056bc07ada0c2655c58b9eaaf`.
- Viewports 320, 375, 390, 430, 768, 1024, 1440 CSS pixels: no observed document horizontal overflow; cost CTA remained onscreen; on 320 mobile with unknown-price option, no left/right overlap in price bar.
- RU/night selected without altering the scene initially; image scene then switched separately to BB.webp; respective `aria-pressed` attributes updated.
- Select `smart_toilet`: count changed 0 → 1, price remained 89 500 € due to unknown cost; select DEMO `floor`: 89 500 € → 92 100 €, +2 600 €.
- DEMO dialog open/close succeeded. No observed browser page errors during these interactions.

## Open gates before merge / any deployment

- In-repository PR review and independent screenshot QA from **the proposed branch build**, not only live CSS injection.
- Verify mobile screenshots at 320/375/390/430, narrow Android/iOS browser and 200% browser text zoom, keyboard/tab flow and text-spacing overrides.
- Confirm full LV/RU font glyph coverage, actual WOFF2 requests, real contrast across all interactive states, CLS/LCP, `prefers-reduced-motion` and theme transition after deployment.
- Verify all forms, .txt download, option dependencies/price details and unknown-price behavior after a deployed preview build.
- Assets' commercial publication rights and manufacturer assertions need separate client confirmation.
- **Do not merge or deploy without the owner's explicit approval of the PR HEAD.**

**Status:** implementation in Draft PR pending owner/QA approval; live Render owner preview untouched.
