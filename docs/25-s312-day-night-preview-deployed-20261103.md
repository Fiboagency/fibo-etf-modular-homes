# ROVELLC S312 — DAY/NIGHT preview deployed

**Дата:** 2026-11-03 (Europe/Riga)  
**Статус:** OWNER-PREVIEW LIVE; PRODUCTION UNCHANGED  
**Задача:** ETF-S312-UXUI-20261103 / frontend integration  
**Публичный тестовый адрес:** https://fibo-etf-atelier-owner-preview.onrender.com/

## Зафиксированный релиз

- Дизайн: `The Destination / Quiet Architecture`, DAY / NIGHT, одна модель S312.
- UX design: [PR #22](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/22), merged.
- Static frontend integration: [PR #23](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/23), merged.
- Preview source revision deployed: `b65c9c646bce1c628c2d6b5ef7a494fa96ad153c`.
- Render workspace: `tea-dba7n2gm7kps73fq8j30`.
- Render static-site service: `srv-dbj7148473hc73bb1k7g`.
- Deploy ID: `dep-dbkrpjrbc2fs73a6kt60`; Render status: **live**.
- Service source branch: `feature/etf-architectural-atelier-ui-20261101`, publish path: `prototype`; auto-deploy remains **off**.
- No changes to `main`, customer production systems, backend, CRM, billing, or real quote flow.
- The deployed `prototype/index.html` references the *existing local assets* (`AA.webp`, `BB.webp`, ROVELLC SVG, S312 schema SVG), not a remote live-preview origin. `noindex,follow` is retained.

## Фактические QA-доказательства после деплоя

**Область проверки:** browser (Firecrawl Chromium), actual deployed URL with cache-busting query. This is NOT an iOS device or independent accessibility certification.

- Public response loads the **new** interface (`.config-studio`, `#themeNight`, `#sceneNight`) rather than old `#siteThemeSwitch`.
- Logo (150 px native view), AA (1678 px) and BB (1679 px) fetched and rendered.
- Browser viewports 320, 390, 768, 1440: **no horizontal overflow**; fixed price bar found in all.
- Four combinations site DAY/NIGHT × photo DAY/NIGHT on mobile: photo and theme independent, demo price unchanged at **89 500 €**.
- Price interaction: curtains **91 300 €**, heated floor **93 900 €**, DEMO LED **94 850 €**. Unknown-price kitchen selection preserves subtotal **94 850 €** and displays quote-warning separately.
- Demo dialog opens, name receives focus, fixed bar hides under dialog, Escape closes and focus returns to trigger.
- Captured page JS errors: **none** during exercised scenarios.
- `robots: noindex,follow`; catalog and conflicting measurements still marked as tentative / manufacturer-source data.
- Do not call demo numbers an ETF offer or treat `S312-C01..C12` as resolved.

## Open work / next tasks

1. **Owner visual review** of published DAY/NIGHT at 390 / 1440 and approval of any additional UX refinements; do not treat a successful deploy as formal client sign-off.
2. **Mobile device QA** on real iPhone Safari (safe area, keyboard, sticky bar, photo crop, animation) and Android; **NOT CHECKED**.
3. **Accessibility QA** including 200% text zoom, keyboard-only, screen reader, focus and modal interaction, full WCAG 2.2 AA criteria; **NOT CHECKED**.
4. **Supplier/client validation** of S312 BOM, height, occupancy, prices, VAT, shipping, engineering documentation, brand/photo licensing, incompatibilities; preserve conflicts `S312-C01..C12`.
5. After owner feedback, any frontend changes require separate branch / PR and explicit preview release approval. Future real multi-model configurator, backend and CRM are **not part of this release**.

## Stage decision

**Preview delivered:** YES. **Production release:** NO. **Frontend QA scoped browser tests:** PASS for tested scenarios; real device and independent review still OPEN.
