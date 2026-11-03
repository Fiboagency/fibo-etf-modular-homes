# S312 owner-preview — Latvian as the default language

Date: 2026-11-03  
Scope: owner-preview `feature/etf-architectural-atelier-ui-20261101` only; no production changes.

## Decision

Every fresh entry or reload of the preview opens with Latvian (`lv`) as the default interface locale, regardless of the previously selected language stored in the browser. The language selector still allows Russian (`ru`) during the current page visit. A deliberate `?lang=ru` deep link is an explicit override and still opens in Russian.

## Implementation

- Keep `<html lang="lv">` and `state.lang='lv'` initialization.
- Stop reading the stored locale from `localStorage`. Older browser storage values containing `lang:'ru'` are safely ignored.
- Stop writing locale to `localStorage`; persist visual theme, AA/BB scene and selected configurator options as before.
- Keep LV/RU dictionary, price formatting, accessibility translations and manual language switching unchanged.

## Acceptance checklist

- [ ] Fresh load with no stored state shows LV in the selector, text, accessibility labels, TXT export and locale-sensitive number formatting.
- [ ] Previously selected RU in older `localStorage` does **not** override LV on a normal reload.
- [ ] Selecting RU immediately updates all translated UI and stays RU for interactions in the current page.
- [ ] Reload after selecting RU returns to LV, preserving configured options and day/night preferences.
- [ ] An explicitly visited `?lang=ru` opens in RU; other links open in LV.
- [ ] Verify mobile/desktop and day/night after owner-approved merge + manual Render owner-preview deploy.

Static source verification of the locale initialization and storage changes is included in the PR. Browser/runtime QA and deployment are **not** claimed complete until tested on the deployed commit.

## Next steps

1. Owner reviews and merges the PR into the **preview feature branch** (not `main`).
2. Manually deploy the preview service (autoDeploy is disabled).
3. Run the acceptance checklist on the live preview, including an existing browser previously left in RU.
