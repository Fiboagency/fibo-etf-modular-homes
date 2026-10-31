# ETF — Architectural Atelier: implementation handoff, v1

Date: 2026-11-01
Owner decision: **Architectural Atelier (Direction A) selected** in this conversation, specifically with further development of brand style and integration of the 10 uploaded images in the configurator.
Authority: **Fibo Agency internal design/prototype approval only**. This does NOT constitute brand-name, prices, commercial rights, scope, production release or client's acceptance.
Source design exploration: [06-premium-brand-art-direction-ru.md](06-premium-brand-art-direction-ru.md).
Code: [prototype/index.html](../prototype/index.html), implemented in isolated branch `feature/etf-architectural-atelier-ui-20261101`.
Parent concept: `feature/etf-photo-brand-exploration-20261101` (PR #2), not merged into main.

## Brand thesis

**Quiet Architectural Luxury:** premium character is conveyed by the architectural photography, careful composition, real materials, restrained editorial typography and precise restrained controls. Visual hierarchy must foreground the house and its finishes; the sales interface is intentionally subordinate. This is appropriate for a considered purchase of a modular residence; it would be too quiet for a racing-sports brand.

## Brand tokens (implemented; still subject to client identity approval)

| Token | Value | Role |
|---|---|---|
| `--stone`, `--paper` | `#F0EDE6` | Warm limestone page |
| `--ink` | `#292C26` | Architectural charcoal text |
| `--forest`, `--accent` | `#314338` | Selection, links, primary CTA |
| `--taupe` | `#A48F76` | Timber-inspired supporting accent |
| `--burgundy` | `#793F46` | Facade-specific secondary accent |
| `--line` | `#D8D4C9` | Borders / separators |
| `--type-editorial` | Georgia, Times New Roman, serif | Distinctive editorial headings |
| Body typography | Segoe UI, Arial, sans-serif | Functional selection, prices, labels |

**Important:** "ETF." text mark is a temporary concept, not an official client logo. No external font binaries are required or committed. Final font licensing and five-locale glyph proof remain open.

## Built components

- Editorial top-bar and hero, photographic stage with distinct overlay labels, three navigation tabs.
- Responsive split composition (photo ~60%, form ~40%) and mobile stacked format.
- Facade image-swatch controls: K.webp anthracite; A.webp natural timber day; B.webp natural timber night; J.webp burgundy.
- Floor image-swatch controls: E.webp oak; G.webp grey; F.webp cherry; H.webp light oak.
- Bathroom presets: C.webp white marble + black matte floor; D.webp taupe stone + warm wooden floor. **No independent arbitrary wall/floor image combinations** without more images or approved layered rendering.
- Three demo-only house sizes, three demo-only furnishing packages, switches for terrace / heat pump, capped counter for roof windows, standard/mirrored layout.
- Live client-side calculation (all prices fabricated and disclosed as such), breakdown, local text-file export and local form demo (never sends PII).

## Visual implementation

- Photograph must keep aspect ratio and natural color; no invented 3D or photo recoloring.
- Desktop hero uses a genuine serif treatment; controls stay humanist/sans; avoid excessive card rounding or glossy shadows.
- Controls support descriptive labels and selected states with both a border and accessible `aria-pressed`, not color alone.
- Images are served directly from `prototype/assets/images/`. Uploaded file provenance: project repository; **rights for external client production use remain UNKNOWN**. The current environment uses images only for internal prototype/review. Do not publish commercially until explicit rights clearance.
- Subtle UI transitions; respect `prefers-reduced-motion`.
- On mobile, stage remains first and controls follow; prices are in the configuration form, not pinned to overlay the content.
- No unapproved copy changes to pricing rules/quotes. Marketing claims are conceptual only.

## Functional QA recorded (isolated browser, before any live preview release)

- Initial demo price: 108000 EUR.
- Facade natural → A.webp, burgundy → J.webp, anthracite → K.webp; natural at night → B.webp; night option disabled for non-natural facades.
- Floors oak → E.webp (108000 EUR); grey → G.webp (108450 EUR); cherry → F.webp (108650 EUR); light oak → H.webp (108350 EUR).
- Bathroom marble preset → C.webp; taupe + warm floor → D.webp; sample total after previously selected light oak: 107700 EUR.
- Demo model switch, premium package, terrace toggle, roof windows counter max=3, request modal open/close — observed working. Final test combination total 141100 EUR.
- No observed uncaught JavaScript errors in tested flows.
- Initial visual desktop screenshot inspected at 1440x1000 RU; mobile screenshot inspected at 390x844 RU. No horizontal page overflow was observed in either viewport.
- Real image load confirmed at 1440px desktop for K/E/C.

## NOT CHECKED / acceptance gates

1. Full WCAG 2.2 audit, color contrast across all photographed backgrounds, accessible keyboard arrow navigation and screen-reader behavior.
2. Real LV/EN/LT/ET/RU application translations (prototype currently RU). Script proof for Latvian accents and Cyrillic must be captured; no claim of five-localization readiness.
3. All model-size imagery: one house image per material for demo; dimensions do not visually change.
4. Final quote/server pricing validation, CRM/email request, anti-spam, GDPR forms and admin panel; none are implemented.
5. SEO, Lighthouse/real mobile performance, image loading network cost (10 WebP files collectively substantial), cache policy and high-density responsive crops.
6. Independent visual QA based on published preview deploy + matching SHA, final art approval, and exact production release authorization.
7. Client-specific copyright/usage clearance for uploaded visuals and official brand/company logo.
8. Exact client catalogue, model drawings, real bills of materials, pricing and VAT rules require client signoff.

## Next steps

1. Owner reviews this implemented draft and requests adjustments.
2. Confirm image usage rights / identify exact owner-facing preview publication scope.
3. Prepare LV/EN/LT/ET/RU localized copy and typography matrix; proper localization in product architecture comes after MVP architecture is approved.
4. Decide whether bathroom needs independently selectable walls and floor (requires more image coverage), and define actual option/model dependency matrix.
5. Design backend validation, administration and lead capture only after scope agreement; use PRs and separate release approval.
