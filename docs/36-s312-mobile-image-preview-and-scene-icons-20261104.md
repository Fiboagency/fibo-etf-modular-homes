# S312 — Mobile contextual preview: large photo and quiet scene icons

**Date:** 2026-11-04 (Europe/Riga)  
**Scope:** Owner Preview only; S312 design refinement; **not merged or deployed**.  
**Request:** Owner's physical iPhone screenshot shows too-small top preview and incongruent bright emoji DAY/NIGHT buttons.  
**Source:** screenshot provided privately in ChatGPT. **Do not commit user screenshot** or any personal browser/status information.

## Observed issue
- Previous compact dock showed a narrow picture ~92–112 px across, alongside the model name and two native emoji buttons. The main house image was not visually prominent.
- The prior “expand” mechanism required a separate tap and rendered a second copy of the image. On smaller phones this consumed valuable space without improving the default presentation.
- Sun emoji appearance was platform dependent and selected state used a large electric-blue square, inconsistent with the ROVELLC quiet-architecture visual direction.

## Changes
- Mobile preview now renders a single full-width house image *by default*, not just a small thumbnail. Photo height is responsive `clamp(136px,24dvh,210px)`; when expanded `clamp(184px,35dvh,292px)`.
- Removed duplicated expanded-image element; the existing expand/collapse button increases the same image. Existing “view full photo” action remains available in expanded mode.
- Model name / expand hint are unobtrusive text on the image with a subtle dark gradient.
- Replace emoji sun and moon glyphs with compact monoline SVG icons (`aria-hidden=true`) and a quiet light pill. Active scene uses the architectural dark charcoal accent; scene accessibility labels and `aria-pressed` remain unchanged.
- DAY/NIGHT controls stay hidden for interior materials, exactly as before.
- No changes to pricing, selections, gallery context lock, other materials, 12 equipment option definitions, responsive fixed bar, languages or downloadable TXT.

## Candidate browser QA
Method: Firecrawl interactive Chromium on existing preview origin using **temporary** GitHub branch HTML/JS via `page.setContent()`, with branch CSS inserted at document head and final CSS fix layered in session. No Render or public content changes.

| Viewport | Default photo size in dock | Fixed price pinned | Horizontal overflow |
|---|---|---|---|
| 320×568 | approx. 281×136 px | PASS | NONE |
| 375×667 | approx. 326×160 px | PASS | NONE |
| 390×844 | approx. 341×203 px | PASS | NONE |
| 430×932 | approx. 381×210 px | PASS | NONE |
| 768×1024 | Mobile dock not rendered | PASS | NONE |

- Photo appears when gallery is in reading area and disappears when configuring equipment.
- 11 material swatches and 12 equipment option buttons preserved.
- DAY/NIGHT buttons both render SVG instead of emoji; keyboard accessible native buttons with pressed semantics.
- Graphite facade day `CC2.webp`; selecting night `CC1.webp`, selecting day restores `CC2.webp`.
- Expand/collapse changes preview height in browser (390×844: 203 ↔ 292 px).
- Expanded action button and scene control **do not overlap** at 320 px after CSS fix; bottom price remains pinned.
- Warm floors still changes base to `92 100 €` in candidate interaction.
- RU aria-label verified, site supports LV/RU translations already; one full physical-device test is still pending.

## Pending and acceptance
- Owner to review design on physical iPhone Safari and Android Chrome (real browser bars, safe areas).
- Independently review screenshot at 320, 375, 390, 430 px; inspect photo crop, font/contrast and inline day/night control in both site themes.
- Test expanded/collapsed keyboard focus at 200% zoom and screen-reader scenarios.
- Status: feature branch **READY_FOR_OWNER_REVIEW**, not a visual or production acceptance certificate.
- `main`, Render Owner Preview and production unchanged by this PR. Merge/deploy require explicit owner confirmation.
