# ETF — Ночные кадры фасадов K / L

**Дата:** 2026-11-01  
**Этап:** включение новых визуализаций фасадов в оба демонстрационных оформления, для внутреннего просмотра Fibo Agency.  
**Источник:** `feature/interactive-configurator-demo-20261101/prototype/assets/images/K.webp` и `L.webp` — новые файлы, добавленные владельцем в исходную ветку. На ветке двух дизайн-вариантов существовал **старый K.webp (дневной антрацит)**, поэтому его заменять было нельзя.

## Наблюдаемое соответствие изображений

| Отделка | День | Ночь |
| --- | --- | --- |
| Натуральное дерево | A.webp | B.webp |
| Антрацит | K.webp (старый дневной кадр) | anthracite-night.webp (новый K.webp из исходной ветки) |
| Бургунди | J.webp | burgundy-night.webp (новый L.webp из исходной ветки) |

Новые бинарные файлы перенесены между ветками GitHub **с использованием существующих Git blob SHA**, без повторного сжатия и без удаления оригинальных дневных файлов:
- `anthracite-night.webp`: `03187074c80dfc365f3809a33ad7ef3ce21ac656` (Git blob SHA исходного K)
- `burgundy-night.webp`: `cc9109de8e0408fd99d5888221c96dfb3f05dadf` (Git blob SHA исходного L)
- Дневной антрацит `K.webp` прежний: `37449ddda76557d76565c891a848d8b648022f3f` (Git blob SHA)

## Реализованное поведение

- Кнопки «День / Ночь» доступны для **трёх** цветов фасада в обоих стилях `?variant=1` и `?variant=2`.
- При смене цвета фасада выбор дневного/ночного света **не сбрасывается**. Это позволяет сравнивать три ночных ракурса подряд.
- При изменении стиля (Вариант 1/2) выбранный фасад и время суток остаются прежними.
- В тёмном варианте **ночной имиджевый кадр в hero соответствует текущему выбранному фасаду**, даже когда в рабочем превью выбран день. Это декоративная презентационная сцена, не изменение конфигурации.
- Во всех версиях примерная цена зависит от тех же опций, что и раньше; дневной/ночной просмотр её не меняет.
- Никакого 3D, динамической подсветки или изменения исходных изображений нет.

## Проверки

В изолированном браузерном preview протестированы все комбинации: антрацит K/anthracite-night, дерево A/B, бургунди J/burgundy-night; тёмный hero синхронизируется с тремя ночными изображениями; стили переключаются без ошибок JS. Визуально просмотрены: ночная бургунди в основном превью, тёмный hero, мобильный 390×844.

## Не утверждено

- Коммерческие права использования изображений и соответствие фактическому продукту ETF остаются непроверенными.
- Реальные цены, локализация LV/EN/LT/ET/RU, полная проверка WCAG, performance и production-приёмка не входят в эту доработку.
- Перед публикацией коммерческого сайта подтвердить лицензию и реальные размеры/материалы.

## Дальнейшие действия

1. Обновить owner-preview Render из ветки после проверки PR.
2. Проверить на реальном опубликованном URL дневную/ночную версию для всех фасадов и светлый/тёмный стиль.
3. Собрать замечания владельца о визуальной подаче night-сцен.

## Фактическая публикация и приёмочный smoke test

- PR #5: https://github.com/Fiboagency/fibo-etf-modular-homes/pull/5 — **merged** только в feature/etf-dual-theme-switcher-20261101, НЕ в main.
- GitHub merge commit: `d770e10efcd2a6f344a9ebe0b813540d04cf7784`.
- Preview-only Render service: `srv-dbjdje6tlv9c73cu00e0` workspace `tea-dba7n2gm7kps73fq8j30`.
- Deploy `dep-dbjdsn3bc2fs73chr3kg` has status **live**, source commit `d770e10efcd2a6f344a9ebe0b813540d04cf7784`.
- URL: https://fibo-etf-dual-concept-preview.onrender.com/?variant=1 and https://fibo-etf-dual-concept-preview.onrender.com/?variant=2
- Actual published URL browser verification, RU:
  - HTTP 200.
  - Daytime initial anthracite K.webp, demonstrational price 108000 €.
  - Night anthracite `anthracite-night.webp` in both themes plus Nightfall hero.
  - Night burgundy `burgundy-night.webp` in both themes plus Nightfall hero.
  - Night natural `B.webp` in both themes plus Nightfall hero.
  - Price unchanged in each lighting/theme transition (108000 € for default other options).
  - Desktop viewport 1440x960, scrollWidth 1425 <= 1440; mobile 390x844, scrollWidth 375 <= 390.
  - No observed JavaScript errors in these interaction paths.
- Full cross-browser, localization, a11y, performance and client production approvals remain NOT_CHECKED. This is **a Fibo Agency demo only**, not the production website.
