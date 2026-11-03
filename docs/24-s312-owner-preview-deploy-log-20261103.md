# ROVELLC S312 — Owner-preview release log
**Дата:** 2026-11-03 · **Этап:** после PR #26 · **Статус:** DEPLOYED TO OWNER PREVIEW, QA PASS FOR CHECKED SCOPE

## Публикация
- Репозиторий: `Fiboagency/fibo-etf-modular-homes`, preview branch `feature/etf-architectural-atelier-ui-20261101`.
- PR #26: https://github.com/Fiboagency/fibo-etf-modular-homes/pull/26 — `merged: true`; `merged_at: 2026-11-03T11:38:32Z`.
- Точный опубликованный commit: `ab9d88b0dfeb0bb17228176d9e6b244a466f0bee`.
- Render workspace `tea-dba7n2gm7kps73fq8j30`, service `srv-dbj7148473hc73bb1k7g` (`fibo-etf-atelier-owner-preview`).
- Deploy ID `dep-dbksg0jncjis73f7msd0`, status `live`, completed `2026-11-03T11:39:58.34439Z`.
- URL: https://fibo-etf-atelier-owner-preview.onrender.com/
- Service is static, linked to preview feature branch, publishPath `prototype`; autoDeploy remains OFF. **No main/production deployment**.

## Проверка LIVE версии
- Firecrawl fetched the live site `HTTP 200`, brand title `ROVELLC S312 — demonstrācijas konfigurators`; rendered content includes new editorial `No pirmā iespaida līdz projektam`, companion BB image and technical disclosure. The current source blob of published commit: `ce70ef975bc0b152afccbede2db9f13915a24836`, content length 60,510 chars.
- Browser real live viewport tests `320×720`, `390×844`, `1440×900`: horizontal overflow absent, photos AA/BB naturalWidth 1678 and 1679 px, mobile only group #03 initially expanded, desktop visual rail visible, B2B story exists.
- Verified option pricing: demo S312 base `89,500 €`, after demo heated floors `92,100 €`, after demo electric curtains `93,900 €`, added unknown-price conditioner keeps demo subtotal `93,900 €` and displays `+ ?`. Breakdown explicitly lists price-on-request conditioner; option selection counter shows 3.
- Verified all four independent combinations of site DAY/NIGHT × scene DAY/NIGHT; alternate companion image AA/BB selected independently. RU translated page title and mobile CTA loaded.
- Demo modal opens; Escape closes and returns focus to `openModal`. No JavaScript page errors in checked scenarios.
- **Live browser note:** at width 320 with selected demo options, bottom price bar ≈95px. A real-device check with mobile keyboard and safe-area is still needed.
- Did not submit a form, place real order, send a client message, or check actual TXT payload bytes. The page remains local TXT-only demo.

## Следующие задачи
1. Owner approval of actual visuals on iPhone (especially DAY/NIGHT transition, scroll and 320px price bar) — OPEN.
2. Physical Safari/iOS + Android device tests, keyboard/zoom/focus and quantitative accessibility/performance checks — OPEN.
3. Source-verified interior photography/rights and final S312 package specs including conflicts in `docs/18` — BLOCKED by manufacturer.
4. Confirmed B2B order process and quote form backend/CRM/email, actual prices/BOM, delivery/mounting/local code implications — OUTSIDE this preview; separate approval and PR required.
5. Once client approves, agree MVP scope and staged build; no online payment required.
