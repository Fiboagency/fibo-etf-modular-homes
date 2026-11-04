# ROVELLC S312 — permanently expanded materials section

**Date:** 2026-11-04
**Status:** prepared in isolated preview feature branch for owner review. Not merged or deployed.

## Owner request
As the left sticky image changes according to the right-hand scroll position (facade / floor / wall / bathroom), keep the first "Konstrukcija un interjers" group of the S312 configurator always expanded so the image/material relation remains visible.

## Implementation
1. Convert only group 01 from a native disclosure `<details>` to a semantic `<section>` with a static `<h3>` and unchanged contents. A permanently expanded section cannot be closed by pointer, keyboard, or other group's state.
2. Preserve the exact existing material and interior option containers and IDs (`finishOptions`, `interiorOptions`). No new photos or changed prices.
3. Keep groups 02–05 as native `<details>`; only one of these four can be expanded at a time. Initially none are expanded, making the material selection the visible starting point.
4. Keep existing selection-count badges for **all five** groups by updating the badge renderer to use either `summary` or the static group heading.
5. Style the new static heading to match existing group headings, including on screens <=600px; no plus/minus icon or false button affordance.
6. Preserve LV/RU i18n, two themes and photo scene toggles, the fixed/mobile price bar, product data, persisted selections and TXT export.

## Static checks
- Verified real GitHub source readback after writing files.
- Exactly one fixed materials section and four remaining native accordions.
- All four remaining accordions initially closed and still mutually exclusive.
- Badge rendering includes fixed heading and four native group headings in original order.
- Existing material option targets and original demo price are present.
- CSS brace balance: PASS.

## Pending visual and functional QA
- Desktop scroll (slow/fast): image changes match facade/floor/walls/bath while first group remains visible.
- Toggle any of groups 02–05; verify group 01 remains present and previously selected material stays selected.
- Mobile 320/375/390 px, DAY/NIGHT and LV/RU labels.
- Badge counts, keyboard and assistive technology, and TXT download. No actual browser test completed in this PR.

## Release boundary
- Review only; no changes to `main`, production, client communication, or Render settings.
- Owner approval of PR HEAD and a separate explicit manual preview deployment approval required.
