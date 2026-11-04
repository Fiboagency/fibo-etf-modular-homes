# ROVELLC S312 — Material Gallery swatch refinement (2026-11-04)

**Scope:** isolated owner-preview design refinement, no production deployment or changes to the configurator logic.

## Owner direction
The desktop reference screenshot showed rigid square tiles and bright selected rectangles in the four material groups. The owner approved a restrained material-gallery presentation to match the existing Soft-Tech Product Gallery / Quiet Architecture interface.

## Change
- All 11 existing material variants remain; no new images or options.
- Replace full-tile borders and inset padding with frameless photographic material samples.
- Rounded material photographs (11 px), labels below, more breathing space.
- Selected state is a fine outline **on the image only**, a small check badge, and stronger label; existing `aria-checked` continues to drive this state.
- Preserve existing brand action accent; no global palette or typography change.
- Desktop 3 columns; small mobile up to 600 px 2 columns.
- Focus-visible remains explicit; reduced-motion suppresses sample transitions.
- Implemented as additive CSS in `prototype/future-living.css`; original inline markup/JS remains untouched.

## Protected
S312 only; current demo totals, unpriced material handling, selected equipment, TXT export, LV/RU, existing photos, stage/gallery state, site theme DAY/NIGHT and independently selectable scene DAY/NIGHT remain unchanged.

## Verification at commit
- Source inspection: updated selectors only in CSS; original HTML/JS unchanged.
- CSS brace balance: PASS.
- Browser/mobile/render/keyboard/contrast validation: PENDING. Do not call this visually approved until after-image review.

## Release
This is a Draft PR aimed at the **owner-preview feature branch**, not `main`; no merge, production, or Render deployment was initiated. A separate owner decision is required for merge/deploy.
