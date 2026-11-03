# ROVELLC S312 — Digital Art Direction Proposal, DAY/NIGHT
**Task:** ETF-ROVELLC-S312-VISUAL-20261103 · **Date:** 2026-11-03 · **Status:** PROPOSAL / OWNER REVIEW · **Run:** FIBO-ART-S312-20261103-01

> **Scope:** redesign the *existing* S312 owner preview only. This is a creative proposal, not approval to implement, merge or deploy. No 18-model catalogue, pricing engine/backend, production, other Render service or main branch changes.

## 1. Evidence and source control
- **Business/source:** [17 business/brand audit](17-rovellc-business-brand-marketing-audit-20261103.md), [18 S312 dossier and conflicts](18-s312-technical-dossier-and-conflicts-20261103.md), [19 cross-role handoff](19-rovellc-s312-cross-role-handoff-20261103.md), `data/s312-source-data-20261103.json`. Manufacturer claims remain *manufacturer claims* and should not be generalized as independently verified local technical, environmental, operating or financial promises.
- **Brief in pending Draft PR #19:** [20 art direction](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/19) and 21 UX/UI configurator specification. The complete current instructions are part of a *Draft PR*, not merged into the base feature branch.
- **Code baseline:** `feature/etf-architectural-atelier-ui-20261101` at `5451ab0344980cab2d8faf8bbc4eadc38e55e2b0`; `prototype/index.html`, `prototype/theme.css`, `prototype/assets/images/AA.webp` and `BB.webp`, `prototype/assets/brand/logo.svg`, `prototype/assets/s312-layout-schematic.svg`.
- **Actually live on Render:** `fibo-etf-atelier-owner-preview`, service `srv-dbj7148473hc73bb1k7g`, workspace `tea-dba7n2gm7kps73fq8j30`; deploy `dep-dbkhf3dg1s2s7388n6n0` of `7ec247b19cc0f7f25fed2565d40df2498b318ee5`, status LIVE on 2026-11-02 23:07 UTC. Auto deploy is OFF.
- **Observed current pixels:** live LV daylight screenshots at **390×844** and **1024×680** captured via Firecrawl 2026-11-03. Both image byte streams were retrieved and viewed. The full dark-theme live screenshot and full-page screenshots were **NOT CHECKED**. The observed mobile page contains a small compact header, editorial Georgia hero, photo with day/night control, four numeric spec tiles (including conflicting height and capacity), and the fixed demonstration-price bar.
- **Confidentiality:** repository is public. Do not add customer's correspondence, business contacts, catalog PDF, unapproved proprietary assets, live prices, unpublished licensing terms or actual leads.

## 2. Art thesis: **The Destination / Quiet Architecture**
**Strategic interpretation, not an approved brand slogan:** ROVELLC S312 is architecture that becomes part of the travel experience. For primary *inferred* B2B audiences (glamping, resort and boutique-hotel owners), the emotional trigger is a distinctive guest unit within nature; the rational reassurance is geometry, layout, transparent configuration and responsible project appraisal. The visitor must recognize an *architectural guest product*, not a space vehicle or an online shopping cart.

**Visual mechanism:** architectural editorial typography; a quiet, light-leading page; truthful large AA/BB photography; deliberate alternation of full-bleed image, white space and technical micro-details; muted mineral/forest materials by day; warm inside/outside lighting contrast against graphite by night. Consistent shared content/IA between both themes.

**Brand-specific negative example:** this atmospheric, destination-focused treatment would be wrong for a price-led mass-market storage-container catalogue: here the S312's distinctive panoramic shape, large-scale setting and guest-use context are central to the product.

## 3. Paired art directions — one coherent brand, two full-site moods
### DAY — Architectural Nature
- Perception: a considered Northern European architecture magazine, calm and tangible.
- Expression: off-white mineral background, deep green text accents, large restrained serif heading; natural images readable without dramatic filter overlays.
- Image: existing `AA.webp`, fully preserve silhouette/roof/supports/glazing and natural camera proportions; never use generated or structurally modified S312 as factual product evidence.
- UI: light parchment surfaces, fine structural borders, quiet CTA and demonstration-price bar. Textual hierarchy *place → product → proof → configuration*.

### NIGHT — Architectural Experience
- Perception: intimate high-end guest experience after sunset, inviting warm interior, quiet outdoor darkness; no neon sci-fi language.
- Expression: deep graphite green, muted amber/limestone highlights, warm restrained strokes, dark but differentiated surfaces for controls, price bar and modal.
- Image: existing `BB.webp`; same model and known nighttime visualization, no fake climate/lighting technology claims.
- UI: every region themed—header, hero, panel, cards, plan, technical data, options, summary, sticky price, dialog, footer—not just a global color inversion.

**Independent protected toggles:** site `themeLight/themeDark` changes site styling only; stage `btnDay/btnEve` changes only AA/BB photo. Valid combinations DAY+AA, DAY+BB, NIGHT+AA, NIGHT+BB. No mutation of selected options, locale, amount or photo when switching UI theme. Preserve circular reveal from theme button **680ms View Transitions**, **580ms** CSS fallback and instant `prefers-reduced-motion`; keep AA/BB crossfade separate.

## 4. Proposed page narrative and keyframes
**1440px full-page order:**
1. 82px brand header: original ROVELLC SVG, subtle product label, site-theme icons, LV/RU.
2. Editorial hero: `S SERIES / S312`, proposed headline «Архитектура как часть путешествия» / `Arhitektūra kā ceļojuma daļa`; 1-2 sentence B2B meaning; no unverified performance promise.
3. Two-column studio: stage left approximately 65–69% of useful width, option studio right. Wide **existing S312 photo** keeps roof/supports and proportions; independent scene control; illustration disclaimer visible.
4. Three trustworthy facts: catalogue **38 m²** covered area, **11.5 × 3.3 m** length/width, one bedroom plus living space, bathroom and balcony. Do not promote conflicting **3.35 vs 3.15 m height** and **3–5 vs 2–3 guests** as settled facts.
5. Collapsible plan **clearly labeled schematic**, not a construction drawing.
6. Configuration studio: model ID, 3 existing explicitly `DEMO_ONLY` priced examples, a different treatment for `SOURCE_CONFLICT` / `PRICE_UNKNOWN`; no fictitious zero increments.
7. Follow-up editorial section: destination context and responsible engineering/commercial inquiry; no fabricated case studies, returns or installation assertions.
8. Footer and persistent price/CTA strip. Current demo request is download-only, never sent to server.
9. Modal download-only dialogue, focus states, error/empty states, both themes.

**390px (priority):** compact header, readable 2–4-line headline, visible whole-house photo, embedded scene control, max 2-column fact grid, full-width option cards and fixed price strip sized around safe area. Use a **separate reviewer-only 390px viewport mode** in the exploratory HTML artifact. Do not make a permanent giant sticky image; later UX should test a compact 'show the house' affordance or small thumbnail.

**320px:** reduce typography and table density; never hide fixed CTA or important demo label; avoid horizontal scrolling. **768px:** a single-column stage then config; **1440px:** two-column editorial layout.

**State specimens to finish before implementation:** modal on/off, selected/unselected demo option, unknown/unsupported option, long LV/RU strings, 4 site/scene combinations, sticky price at scroll/keyboards, all on day/night. A concept prototype is *not* independent QA of those requirements.

## 5. Candidate visual tokens (art proposal, not official brandbook)
| Role | DAY | NIGHT |
| --- | --- | --- |
| `bg` | `#EEEFE8` | `#131D1C` |
| `surface` | `#FAFAF5` | `#1B2826` |
| `elevated` | `#FFFFFF` | `#24322E` |
| `text-primary` | `#25352B` | `#F3F1E9` |
| `text-muted` | `#5D6B60` | `#C3CDC3` |
| `border` | `#CFD7CC` | `#55655A` |
| `accent` | `#3B6350` | `#D8BD97` |
| `cta-primary / text` | `#203E31 / #F7F5EA` | `#D8BD97 / #131D1C` |
| `price-bar` | `#203E30` | `#0D1715` |
| `illustration matte` | `#26372E` | `#0B1516` |
| `focus` | candidate `#DFAA64` | candidate `#DFAA64` |
| `error/success/overlay` | define per component and measure | define per component and measure |

**Measured static pair checks in sandbox** (calculated from proposed hex values; not a full visual WCAG audit): DAY primary/background 11.18:1; DAY muted/background 4.86:1; DAY accent/background 5.88:1; NIGHT primary/background 15.22:1; NIGHT muted/background 10.52:1; DAY price text/bar 10.71:1. Other component combinations, image overlays, disabled, borders, focus, dynamic states and font metrics **NOT CHECKED**.

**Typography:** display serif is an editorial *direction*; exploratory HTML uses system Georgia/Times and Arial fallback. A final commercially licensed family/font and real Latvian + Cyrillic glyph coverage is **NOT APPROVED**. Test `ā č ē ģ ī ķ ļ ņ š ū ž` and `ё й ъ ы щ` at actual 320/390/768/1440 widths.

## 6. Artwork, hero treatment, provenance and rights
| ID | Current source | Proposed use | Rights |
| --- | --- | --- | --- |
| ROVELLC S312 AA | `prototype/assets/images/AA.webp` | DAY image (may also appear in NIGHT UI) | `UNKNOWN` beyond current owner-preview |
| ROVELLC S312 BB | `prototype/assets/images/BB.webp` | NIGHT image (may also appear in DAY UI) | `UNKNOWN` beyond current owner-preview |
| ROVELLC logo | `prototype/assets/brand/logo.svg` | Header identity | `UNKNOWN` beyond current owner-preview |
| S312 schematic | `prototype/assets/s312-layout-schematic.svg` | Clear schematic, never blueprint claim | `UNKNOWN` beyond current owner-preview |
| Catalog photography/PDF | client-provided 2026 LV catalog, NOT copied | reference only pending permission | `UNKNOWN` |
| Additional angles / interiors | not approved and not collected | separate storyboard/production stage | `NOT_AVAILABLE` |
| Commercial font | not selected | license/glyph validation before deployment | `UNKNOWN` |

**Crop/focal point:** original AA/BB approx 1.79 landscape ratio. Desktop 1440: use intrinsic proportions or contain, never cut off physical model edges; 768: maintain whole model with letterboxing if necessary; 390/320: choose contain to keep complete body, allow fullscreen/zoom affordance rather than crop the roof or panoramic terminal glass. No geometry swaps, windows/lighting changes, furniture teleportation or fictional 'heated floor changes exterior' visualization.

## 7. Actual exploratory visual artifact
`ROVELLC_S312_DAY_NIGHT_art_preview.html` was created **in the ChatGPT working files**, **not committed into the repository**. It is a standalone, browser-openable interactive *concept* with independent site/photo toggles, candidate full-page layouts and LV/RU, options and demo math, a small 390px review mode, price bar, and local .txt-only example request. Its images are **linked** to the already-existing owner-preview URLs, not duplicated or licensed anew.

- **Proof SHA256 (local file bytes):** `574d305604d7439742e2712fa8a9f010df99d537710956f24123e00a5ed66592`.
- **Sandbox-only browser checks:** selection of curtains changes demo from 89,500 to 91,300 EUR; separate NIGHT photo and NIGHT theme switches remain independent; LV hero renders; review mode 390px; no horizontal overflow in 320px simulator; modal opens; sticky price is viewport fixed. Browser testing used local HTML with remote images blocked by sandbox networking; this **does not** verify the composed visual with AA/BB or real iOS behavior.
- **Production fidelity:** not a drop-in patch, not client-ready, no valid server submission; do not mistake concept handlers for deployed production functionality.

## 8. Open issues / owner review
1. Approve or revise the thesis **The Destination / Quiet Architecture** and candidate headline. This is a positioning proposal, not brand approval.
2. Check the visual preview in an online browser, including AA/BB image loading and all DAY/NIGHT combinations. Full-page desktop/mobile captures of the concept and cross-browser artistic review remain pending.
3. Confirm who may use/export public visuals and logo; preserve `UNKNOWN` rights until approval.
4. Supplier/product owner resolves `S312-C01..C12`: height, occupancy, included/optional BOM, upgrade compatibility and real pricing. No price-sheet import.
5. UX designer aligns component states to pending [PR #19](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/19) after approval; product/engineering, accessibility, localized text and mobile price/keyboard checks are separate gates.
6. Only *then* implementation in a different feature branch + Draft PR. No release/merge/deploy authorization here.

## 9. Pilot provenance and status
- `fibo-digital-art-director` **v0.2.2** / `CHATGPT_SKILL_WORKFLOW`; mandatory role, system prompt, safety, K02/K03/K10, source register and visual verification read at pinned source revision `7288045be692352d008d0168e89617776933b5a9`; bundled role/library remain DRAFT, other K modules not installed.
- **Preparation:** READY (mandatory reads completed; hashes of bundled text NOT_CHECKED, expected manifest only).
- **Visual analysis:** PARTIAL, actual viewed live screenshots LV DAY 390×844 and 1024×680; existing NIGHT, 1440 complete page, interactions in real Safari NOT CHECKED.
- **Task result:** PARTIAL, interactive design artifact and handoff text prepared; image+UI composed screenshot proof with rights and owner selection still missing. No independent visual or technical QA, no owner concept approval, no Render code/deploy.
