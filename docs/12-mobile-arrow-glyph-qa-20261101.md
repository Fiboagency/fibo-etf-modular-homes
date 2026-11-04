# ETF mobile arrow glyph refinement — 2026-11-01

## Scope and source
- User observed bright blue arrows on a physical phone in the SIA ETF owner preview. Platform/OS screenshot not supplied in this task.
- Public preview: https://fibo-etf-atelier-owner-preview.onrender.com/
- Target Render service: `srv-dbj7148473hc73bb1k7g`, workspace `tea-dba7n2gm7kps73fq8j30`, branch `feature/etf-architectural-atelier-ui-20261101`, auto-deploy off.
- Last live deploy before change: `dep-dbjfqk142hec73ct82ig`, commit `bfe2ed01f984ee02aa1318790238fe16ec294c63` (live).
- Design direction: approved Architectural Atelier (day) / Nightfall (night), original ETF-only header, Fibo Agency footer attribution.
- Art-director pilot reading record: `Fibo Digital Art Director 0.2.2`, source revision `7288045be692352d008d0168e89617776933b5a9`, full role and prompt, K02, K03, K10, source register and visual-verification read. Research seeds, not a certified G5/6 library.

## Diagnosis
- 6 native Unicode arrows in `prototype/index.html`: selected-config heading (↘), two CTA buttons (↗), mobile up-scroll action (↑), config download button (↓), form download button (↓).
- Unicode U+2197/U+2198 can take emoji vs. text rendering depending on font/platform. The client's observation is consistent with iOS emoji fallback, although actual Safari pixels are **not independently captured**.
- The arrow decorations should be brand-neutral and subordinate to architectural typography, not colorful operating-system emoji.

## Implementation
- Replaced all 6 Unicode arrow characters with small, inline SVG arrow shapes using `stroke="currentColor"` and lightweight `.editorial-arrow` sizing.
- SVGs are marked `aria-hidden=true`, `focusable=false`; labels remain readable to assistive technologies.
- Added LV/RU mappings for the two labels whose old text included a leading arrow: `Посмотреть изменения` and `Скачать конфигурацию (.txt)`.
- Existing theme controls, Fibo Agency footer, ETF-only header, visualization/photo assets, quote and form logic remain unchanged.
- No 3D/images or additional external assets introduced.

## Acceptance
- At widths 320, 375, 390, 430 and tablet 768, both themes: no blue emoji-style arrows, no new horizontal scroll or clipping. Arrow color follows text and remains readable.
- Switching LV/RU: mobile view-change action and download label fully translated; real click behaviors unchanged.
- Confirm preview commit/render-deploy identity, screenshot actual updated version and inspect screenshots before release.
- Do not claim native iOS visual proof without physical Safari capture.

## Status
Implementation on isolated fix branch; review and Render live verification pending.
