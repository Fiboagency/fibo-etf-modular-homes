# ROVELLC S312 — Material Gallery / Render Preview deployment

**Date:** 2026-11-04 (Europe/Riga)
**Status:** `PUBLISHED_ON_OWNER_PREVIEW` — Render API `live`, not production acceptance.

## Source and release evidence
- GitHub PR: https://github.com/Fiboagency/fibo-etf-modular-homes/pull/37 — confirmed merged.
- PR merge commit: `fbd5e40702dbe1c1fca76281a09521870ea2d747`.
- Owner-preview Render service: `fibo-etf-atelier-owner-preview` (`srv-dbj7148473hc73bb1k7g`), workspace `tea-dba7n2gm7kps73fq8j30`.
- Service linked to repository `Fiboagency/fibo-etf-modular-homes`, branch `feature/etf-architectural-atelier-ui-20261101`; auto-deploy disabled.
- GitHub compare on release: branch identical to approved PR merge commit (ahead/behind = 0).
- Manual deployment authorized by owner in project conversation ("да, запустить").
- Triggered with unchanged build cache and Render API. Deploy ID: `dep-dblk02gae00c73cfiq9g`.
- Render API returned status `live`, commit `fbd5e407...`, finished `2026-11-04T14:24:23.524559Z`.
- Published URL: https://fibo-etf-atelier-owner-preview.onrender.com/
- No production service, main branch, environment values or pricing logic changed.

## Delivered
- CSS-only Material Gallery styling: borderless material photography, rounded previews, understated selection outline/check mark, 3-column desktop and 2-column narrow mobile view.
- All original 11 swatches, images, captions, pricing and DAY/NIGHT behavior retained in source; details in `docs/29-s312-material-gallery-swatches-20261104.md`.

## Verification and remaining tasks
- **PASS:** GitHub PR merged, source branch SHA verified, Render service identified, Render deploy `live`.
- **NOT_CHECKED:** independent post-deploy screenshot comparison for desktop/mobile and both themes. An attempt to fetch public CSS using web access was unsuccessful; do not infer a full browser visual QA pass.
- **NEXT:** owner review of swatches, layout and legibility on desktop/mobile.
- **NEXT:** test selected-state persistence, tab/focus, reduced-motion, DAY/NIGHT, LV/RU and unknown-price selections against live preview.
- **NEXT:** verify real-device narrow width and contrast before any client-facing acceptance or production release.

This document records the actual deployment only. It is not a production release authorization.
