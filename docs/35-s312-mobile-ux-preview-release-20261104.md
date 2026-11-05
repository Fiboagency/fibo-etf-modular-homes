# ROVELLC S312 — Mobile UX owner-preview release

**Date:** 2026-11-04, Europe/Riga  
**Stage:** Owner-review interactive prototype  
**Status:** Render deployment **LIVE**, scoped browser smoke test **PASS**, physical-device acceptance pending.

## GitHub release source
- Functional change: PR #43, https://github.com/Fiboagency/fibo-etf-modular-homes/pull/43
- PR #43 merged into `feature/etf-architectural-atelier-ui-20261101`.
- Merge SHA: `56619116d97eb119ea1b6641aa5939611f8561d7`.
- GitHub compare of source branch vs merge SHA: identical (ahead 0, behind 0).
- Audit and design contract: `docs/33-s312-mobile-ux-audit-vs-mycabin-20261104.md` and `docs/34-s312-mobile-ux-improvements-implementation-20261104.md`.

## Render release
- Preview static service: `fibo-etf-atelier-owner-preview`, ID `srv-dbj7148473hc73bb1k7g`.
- Workspace ID: `tea-dba7n2gm7kps73fq8j30`.
- Manual deploy triggered; service auto-deploy stays disabled.
- Deploy ID: `dep-dbln0khsrm7s73f40450`.
- Deployed SHA: `56619116d97eb119ea1b6641aa5939611f8561d7`.
- Render API finished `2026-11-04T17:50:35.898759Z` with status `live`.
- Public owner-preview URL: https://fibo-etf-atelier-owner-preview.onrender.com/
- Production and `main` untouched.

## Post-release smoke test
Method: Firecrawl/Playwright live browser at published Render URL, browser viewport `320x568` with reload and scroll to facade swatches.

**PASS:** dock becomes visible, bottom pricebar stays pinned, exactly 1 shared material pricing disclaimer, 11 swatches, 12 equipment buttons, no horizontal overflow, expanded dock works and shows the image, no reported JavaScript `pageerror`.

## Pending acceptance
- Real iPhone Safari/Android Chrome screenshots including 320x568, 375x667, 390x844 and 430x932.
- Exact visual comparison of material photos, LV/RU and DAY/NIGHT in compact and expanded modes.
- iOS safe-area / keyboard / scrolling behavior, 200% text zoom, reduced-motion, VoiceOver/TalkBack.
- Owner visual approval; avoid any production release claim.

This document is read-only release evidence, not a code update or approval for production.
