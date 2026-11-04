# ROVELLC S312 — permanent materials panel published to owner preview

**Date:** 2026-11-04 (Europe/Riga)
**Status:** `OWNER_PREVIEW_LIVE` (not production release or visual QA pass)

## Delivery evidence
- Feature PR: https://github.com/Fiboagency/fibo-etf-modular-homes/pull/39 (merged).
- Merge SHA: `f4a987e04f0d468d2f5e3015d541b9fe69ecebaa`.
- GitHub source branch `feature/etf-architectural-atelier-ui-20261101` matched the merge SHA when checked (identical).
- Render service: `fibo-etf-atelier-owner-preview` (`srv-dbj7148473hc73bb1k7g`), workspace `tea-dba7n2gm7kps73fq8j30`.
- Manual deploy triggered with auto-deploy disabled, no build-cache clearing.
- Deploy ID: `dep-dblk4om1egvs73fh5adg`.
- Deploy commit: `f4a987e04f0d468d2f5e3015d541b9fe69ecebaa`.
- Render API deployment status: `live`, completed 2026-11-04T14:34:24.634743Z.
- URL: https://fibo-etf-atelier-owner-preview.onrender.com/

## Scope
- Materials group 01 always visible with static heading; other groups 02–05 stay collapsible.
- Selected option badges work through the updated selector.
- No price, model, material catalog, language, imagery, DAY/NIGHT logic, production branch or production service changes.

## Next verification
- Real desktop/mobile screenshots of scroll-linked facade/floor/wall/bath visuals.
- Verify group 01 remains open when 02–05 are toggled, including keyboard navigation.
- Confirm LV/RU, day/night, saved selections, unknown-price handling, total and TXT export.
- Independent device QA before owner acceptance of this visual iteration.

Deployment success does not substitute for browser/UI or accessibility testing.
