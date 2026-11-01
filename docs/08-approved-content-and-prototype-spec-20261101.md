# SIA ETF — owner-approved implementation specification (presentation prototype)

Date: 2026-11-01. Status: **APPROVED BY FIBO AGENCY OWNER FOR OWNER PREVIEW ONLY**.
Scope: Existing static presentation prototype at https://fibo-etf-atelier-owner-preview.onrender.com/ only. This document records 33 approval answers: 32 functional/content decisions plus final go-ahead.
This is NOT SIA ETF approval of prices, real products, client branding, terms, paid deployment or full MVP.
Release: direct phased updates to the existing **fibo-etf-atelier-owner-preview** service from branch `feature/etf-architectural-atelier-ui-20261101`. Render service `srv-dbj7148473hc73bb1k7g`, workspace `tea-dba7n2gm7kps73fq8j30`. **Never touch main, production or other services.** No backend or data submission.

## Approved decisions / exact requirements

01. Work only on current interactive concept prototype; keep demonstration prices and functionality.
02. Target audience: show premium Architectural Atelier prototype to SIA ETF; remove internal jargon, preserve accurate demo warnings.
03. Keep original numeric EUR rates/formulas. Headline: **«Демонстрационный расчёт»**. Note immediately by total: **«Цены приведены только для демонстрации и не являются предложением SIA ETF. НДС не согласован.»**. LV equivalent; never present as genuine offer.
04. Main CTA: **«Посмотреть демо-заявку»**. Open modal with name, email and **«Скачать демо-заявку»**. Local TXT download only; explain no server transmission.
05. H1: **«Настройте модульный дом под себя.»** Subhead: **«Выберите размер дома, фасад, материалы интерьера и комплектацию. Посмотрите визуализацию и демонстрационный расчёт стоимости.»**
06. Remove **«У каждой детали свой характер.»** and related repetitive paragraph. Retain compact, dynamic **«Выбранная конфигурация»**.
07. Configurator H2: **«Параметры дома»**; subhead: **«Выберите материалы и комплектацию. Изменения отразятся на визуализации или в демонстрационном расчёте.»**
08. Size group: **«Размер дома»** and 60/80/100 m² only; no Compact/Living/Family or «Один вариант» badge.
09. Facade: anthracite, natural timber, burgundy; remove «Включено». Move Day/Night control next to the large visual; night only when natural timber, using existing asset B.webp.
10. Floors: retain four images/prices; oak reads **«Дуб · Без доплаты»**, others +450/+650/+350 €.
11. Bathroom H3 **«Отделка ванной»**, explanation **«Выберите один из готовых вариантов отделки»**. Preserve two real demo image presets and +2100/+1450 €. Remove decorative subtitles.
12. Packages Basic, Comfort, Premium and descriptions remain; «В базе» → **«Без доплаты»**; shared label **«Доплата к базовой комплектации»**. Do not add +8900 and +17900 to one another; mutually exclusive.
13. Preserve terrace (+6200 €), heat pump (+3900 €), roof windows (+1100 €/unit, max 3). Remove «Демонстрационная инженерная опция». Break layout Standard/Mirrored into subgroup **«Планировка»**.
14. Under photos **«Изображения демонстрационные и не подтверждают технические характеристики дома.»**. The separate pricing warning is mandatory.
15. Header «ETF. / MODULAR HOMES» + **«Демонстрационный прототип»** (localized LV); remove internal-view flags, concept index and extraneous numbering. Footer **«Концепция для SIA ETF · Fibo Agency»**; warnings remain near functions.
16. Full RU/LV UI, including price breakdown, form, error messages, option labels, downloaded file; language selector styled to brand. EN/LT/ET excluded from this phase.
17. LV default on first opening; RU selectable. Language change must preserve currently selected house/options/price.
18. `noindex, follow` on preview; publicly accessible at direct URL (not password-protected). Check live HTML.
19. All ten provided AI illustrations approved for **presentation only**; not verified real houses or unrestricted commercial license. Preserve originals and option mapping.
20. Remove English «Architecture to live in» slogan, keep ETF. / MODULAR HOMES.
21. Two separate CTA actions: primary demo modal, secondary direct **«Скачать конфигурацию (.txt)»** (no PII).
22. Downloaded TXT includes all selected house parameters, line-item pricing breakdown, total and demo/tax warning. PII only in completed modal form; direct file has no PII.
23. Form name/email required; validate nonblank name and valid email; localized specific corrections; post-download status **«Демо-заявка скачана. Данные не отправлены».** No server submission, no persistence of PII.
24. Download in active UI locale. All system strings, option names, breakdown and warnings localized, while user-supplied name/email are unchanged.
25. Visual scenes: changing facade→Facade, floor→Interior, bathroom→Bathroom; manually selectable three tabs. Model, packages, options and layout do not force scene.
26. Full itemized demonstrative cost always visible; dynamic; 0 € entries read **«Без доплаты»**. Preserve arithmetic.
27. Summary dynamic tags include size, facade, floor, bathroom, package, enabled add-ons and layout; hide disabled add-ons.
28. Mobile: visual above options, add **«Посмотреть изменения»** action to jump back to current scene; no sticky image; desktop current split layout.
29. Default: 80 m², anthracite, oak, marble/black bath, Comfort, heat pump on, 1 roof window, terrace off, standard layout. Demo total **108000 EUR**.
30. Persist selected configuration in local browser storage across reload; **«Сбросить настройки»** restores defaults (108000 EUR); do not persist name/email. Keep same configuration across RU/LV.
31. QA: functional controls, all price permutations, RU/LV strings and downloads, desktop/tablet/mobile, keyboard/focus/contrast, JS console, no server request. No claim of WCAG certification.
32. Phased direct publication to **existing owner-preview** Render only. Preserve default branch/main and other services.
33. Owner explicitly approved the whole set for implementation.

## Acceptance tests

- [ ] Exact RU copy above and accurate idiomatic LV equivalents; `<html lang>`, dynamic language values, alt/aria, browser UI and TXT use appropriate locale.
- [ ] Initial total = 92,000 + 8,900 + 0 + 2,100 + 3,900 + 1,100 = 108,000 €.
- [ ] Grey floor = 108,450; cherry = 108,650; light oak = 108,350 from initial.
- [ ] Basic/Comfort/Premium exclusive; add-ons and windows (0–3) exactly adjust total.
- [ ] Day/Night is available only for natural wood; B.webp shown at night; 10 existing assets unchanged.
- [ ] Every selected parameter appears in dynamic summary and in downloaded file; only enabled optional features appear in visual pills.
- [ ] Direct TXT contains no name/email; modal TXT contains fields entered by user; name/email never saved to storage or sent to a server.
- [ ] LV loads first, selector RU↔LV retains price/options and updates screen readers' document language.
- [ ] Refresh retains selection; reset restores 108,000 and initial configuration.
- [ ] No duplicate emotional blocks, internal preview text or English slogan in live page.
- [ ] Hero, all label buttons and footer match final approvals; demo image and price disclaimers remain visible in context.
- [ ] Mobile button returns to visual without breaking selected tab; usable keyboard, focus and form errors.
- [ ] `noindex,follow` present in live HTML; only approved owner-preview service deployed, `main` untouched.

## Release log

Use commit SHAs and Render deploy IDs as immutable evidence. After each deploy confirm `live` and run real public URL checks; do not claim untested flows pass.
