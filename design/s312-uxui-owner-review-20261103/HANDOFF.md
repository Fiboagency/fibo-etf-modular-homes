# ROVELLC S312 — UX/UI Owner Review и frontend handoff

**Task ID:** ETF-S312-UXUI-20261103  
**Дата:** 2026-11-03 · **Ревизия дизайна:** UXUI-v1 · **Решение:** PROPOSED FOR OWNER REVIEW, не утверждённая реализация.  
**Ветка:** `design/s312-quiet-architecture-owner-review-20261103` → base `feature/etf-architectural-atelier-ui-20261101`.  
**Базовый коммит:** `264c8add7a7b411dfc692ef4dd1dbbe9727017d3`.  
**Арт-направление:** The Destination / Quiet Architecture (APPROVED). Дизайн и UX ещё требуют отдельного согласования.  
**Scope:** одна модель ROVELLC S312; статический интерактивный концепт, не production.

## 1. Реально просматриваемые материалы

- [Интерактивный прототип](index.html) — отдельный HTML с DAY/NIGHT по всему сайту, LV/RU, двумя независимыми переключателями, конфигуратором, модальным демо-запросом и локальным TXT.
- [DAY / Desktop 1440](screenshots/desktop-day-1440.jpg)
- [NIGHT / Desktop 1440](screenshots/desktop-night-1440.jpg)
- [DAY / Mobile 390](screenshots/mobile-day-390.jpg)
- [NIGHT / Mobile 390](screenshots/mobile-night-390.jpg)

Четыре изображения сняты с реально загруженными исходными `AA.webp`/`BB.webp` в браузере Firecrawl (Chromium, 2026-11-03). Они **не** являются независимым тестом на настоящем iPhone. HTML подгружает оригинальные публичные preview-ресурсы по HTTPS; для офлайн-просмотра нужна отдельная сборка разрешённых ассетов. Никакие новые вариации геометрии дома не созданы.

## 2. Источники и неизменяемые ограничения

- `docs/17-rovellc-business-brand-marketing-audit-20261103.md`: B2B hospitality — маркетинговая гипотеза, не факт, подтверждённый интервью.
- `docs/18-s312-technical-dossier-and-conflicts-20261103.md`: источники производителя и конфликты `S312-C01..C12`.
- `docs/22-s312-digital-art-direction-proposal-20261103.md`: approved art тезис и предварительные токены.
- `docs/23-s312-approved-art-to-ux-handoff-20261103.md`: ограничения логики, scope и release gate.
- `docs/21-s312-ux-ui-configurator-day-night-redesign-brief-20261103.md`: на момент создания находился **только в открытом Draft PR #19**.
- `data/s312-source-data-20261103.json`: исследовательский JSON; *не production seed*, цены для реальных SKU равны `null`.
- `prototype/index.html`, `prototype/theme.css`: существующая фича с переключением сайта 680ms (View Transition) / 580ms (fallback).
- Изображения по текущим URL preview: `/assets/images/AA.webp`, `/assets/images/BB.webp`; SVG: `/assets/brand/logo.svg`, `/assets/s312-layout-schematic.svg`. Не редактировать/перегенерировать без отдельного разрешения.

Первичные `docs/01..04` отсутствуют в ветке, **SOURCE_UNAVAILABLE**. В публичный репозиторий не переносить переписку, каталог PDF, контакты, прайс-листы клиента.

## 3. Основной пользовательский сценарий

**Гипотеза:** владелец глэмпинга или бутик-отеля → видит архитектурную сцену → сверяет категориальные факты → раскрывает схему → формирует комплект по тематическим группам → видит неизменную DEMO-панель → сохраняет конфигурацию как .txt → обращается к менеджеру отдельно за настоящим инженерно-коммерческим предложением. Вторичный частный покупатель следует тому же процессу, без расчёта окупаемости или ложного checkout.

**Новая IA в единой странице:** компактный header (логотип, тема сайта, LV/RU) → editorial hero → существующая AA/BB stage c независимым переключателем изображения → три продуктовых блока (площадь/размеры/помещения) → раскрываемый схематический план → предупреждение о конфликтах → **шесть** групп конфигуратора → сводка выбранного → editorial секция о проверке проекта → подвал. Постоянная нижняя цена и действия поверх содержимого.

## 4. Два самостоятельных состояния внешнего вида

| Семантический токен | DAY · Architectural Nature | NIGHT · Architectural Experience |
|---|---|---|
| bg | `#EEEFE8` | `#131D1C` |
| surface | `#FAFAF5` | `#1B2826` |
| elevated | `#FFFFFF` | `#24322E` |
| text-primary | `#25352B` | `#F3F1E9` |
| text-muted | `#58695D` | `#C3CDC3` |
| border | `#CFD7CC` | `#55655A` |
| accent | `#3B6350` | `#D8BD97` |
| CTA | `#203E31` / `#F7F5EA` | `#D8BD97` / `#131D1C` |
| fixed-price | `#203E30` | `#0D1715` |
| focus candidate | `#DFAA64` | `#DFAA64` |

Финальное подтверждение контраста каждого компонента, в т.ч. focus/error/disabled, ещё требуется. Текст hero — Georgia fallback, технический sans — Arial/системный. Не заменять собственный ROVELLC SVG логотип. Проверить лицензионные шрифты и RU/LV глифы перед реализацией.

## 5. Модель состояний и реакции

`{theme: day|night, scene: day|night, lang: lv|ru, selected: Record<option_id,boolean>, pricingMode: demoSubtotal|quoteOnRequest, modalOpen:boolean, planOpen:boolean, priceDetailsOpen:boolean}`

1. **Theme control** `#themeDay/#themeNight`: меняет ВСЮ палитру (header/hero/cards/config/plan/price/modal/footer), но не scene, опции, цены или язык. 680ms круговое раскрытие от точки кнопки, fallback 580ms, при `prefers-reduced-motion` — без перехода. Пара `aria-pressed`.
2. **Scene control** `#sceneDay/#sceneNight`: меняет только существующую AA/BB фотографию с мягким crossfade; не меняет theme/price/selection/lang. Четыре независимые комбинации обязательны. Фото не меняется от подогрева пола, штор или иных опций без соответствующих исходных рендеров.
3. **Language** LV (по умолчанию) ↔ RU сохраняет выбор и сумму; `html lang`, названия кнопок и ошибок переключаются. EN/LT/ET — только потенциальное расширение.
4. **Demo priced selections** включаются/выключаются независимо, пересчёт синхронен, `aria-pressed`. Базовая демонстрационная величина **89 500 €**. Шторы `+1800`, подогрев `+2600`, LED `+950`; три вместе дают **94 850 €**.
5. **Unknown-price candidate** допускается в набор с маркировкой «Цена по запросу» и отдельным предупреждением, но не даёт `+0 €`. Отображаемая сумма = **учебный subtotal ТОЛЬКО известных DEMO-слагаемых**, не финальная стоимость. Production должен показывать `quote_on_request` и не обещать точного total.
6. **Persistence:** `localStorage` содержит только тему, сцену, язык, выбранные option IDs. Контактные данные формы никогда не сохраняются там или на сервере.
7. **Plan**: нативный `details/summary`; файл `s312-layout-schematic.svg` подписан как упрощённая схема, не BIM/CAD.
8. **Modal**: `dialog.showModal`, фокус в имени, Esc/закрытие/возврат фокуса; валидация имени/email; скачивание локального `.txt` по текущим опциям, без HTTP/CRM/email и без сообщения «заявка получена».
9. **Price bar**: `position:fixed`, `safe-area-inset-bottom`, DEMO-пометка рядом с суммой, `Состав` раскрывает строки/предупреждение, `Демо-заявка` открывает локальный диалог. При modal поверх bar приоритет у dialog; проверить поведение viewport с реальной мобильной клавиатурой (НЕ ПРОВЕРЕНО).
10. **Mobile house return:** небольшая плавающая кнопка/thumbnail `#mobileJump` появляется при прокрутке конфигуратора и прокручивает к stage; не перекрывает цену. На desktop не нужна; не «липкая» большая фотография.

## 6. Конфигуратор: группы и происхождение

| Группа | Элементы и ID | Дизайн-статус |
|---|---|---|
| 01 Модель и архитектура | только S312, 38 м² покрытой площади, 11.5 × 3.3 м; цвета/размеры не объявлены | OBSERVED_CATALOG / PENDING SKU |
| 02 Конструкция и интерьер | сведения о каркасе, остеклении и отделке — список изготовителя; `smart_toilet` | SOURCE_CLAIMED, price_unknown |
| 03 Климат и комфорт | `floor` (+2600 DEMO), `air_conditioner`, `water_heater` | DEMO_ONLY / SOURCE_CONFLICT / price_unknown |
| 04 Управление и мультимедиа | `curtains` (+1800 DEMO), `lights` (+950 DEMO), `projector_screen`, `voice_control` | DEMO_ONLY / LED_NOT_CONFIRMED / price_unknown |
| 05 Меблировка | `furniture_package`, `kitchen` | OPTIONAL_SOURCE, availability/price unknown |
| 06 Инженерия и услуги | `electrical_international`, `entrance_stairs` | price_unknown, requires engineering & supplier |

**ID mapping инженерной реализации:** `floor → opt_floor_heating`; `curtains → opt_electric_curtains`; `lights` — только DEMO ID без утверждённого SKU; другие UI IDs нужно сопоставлять с идентичными `opt_*` полями из `data/s312-source-data-20261103.json`, **не** использовать display name как API key.

**Компонент OptionCard** должен поддерживать семантику `included_confirmed`, `optional_priced_confirmed`, `optional_price_unknown`, `source_conflict`, `unsupported`, `demo_only` плюс interaction `default/selected/focus/disabled/error`. Прототип демонстрирует demo_only, uncertain/unknown и selectable states; **не все supplier-dependent состояния заполнены реальными данными**. Нельзя выдавать candidate за утверждённую базовую спецификацию. Для unsupported — disabled + объяснение причины после утверждения матрицы совместимости.

## 7. Факты и открытые конфликты

**Можно показывать с точной атрибуцией:** S312, длина 11.5 м, ширина 3.3 м, 38 м² *покрытой* площади; заявленная производителем программа помещений (спальня, гостиная, ванная, балкон). **Требуют подтверждения:** высота 3.35/3.15, вместимость 3–5/2–3, материалы стен, толщина утепления, 12 кВт/фазы, реальный BOM, опциональность оборудования, лицензионные права, VAT, доставка и монтаж, инженерная применимость для Латвии, импортер/гарантия. Не публиковать сертификаты, нормативную зимнюю пригодность, доходность, разрешительный статус или транспортные обещания без доказательств.

## 8. Адаптивность и доступность

| Viewport | Макет | Бар/фокус/медиа |
|---|---|---|
| 1440 | stage и studio двумя колонками; editorial hero над ними | Фиксированный нижний бар; фотография не обрезает корпус |
| 768 | stage и config последовательно, одна колонка | Цена фиксирована; schema развертывается естественно |
| 390 | компактный header; 2-колоночные факты; секции-accordion; floating preview return | Фото `contain`; бар с суммой и действием; `safe-area` |
| 320 | уменьшить сетку и typography, переносить длинные подписи LV/RU | Нет X overflow; сумма/CTA не обрезаны |

Целевой ориентир **WCAG 2.2 AA**, без заявления полного соответствия. Обязательны реальные проверки `2.4.7 Focus Visible`, `2.4.11 Focus Not Obscured`, `1.4.10 Reflow`, `1.4.11 Non-text Contrast`, `2.5.8 Target Size`, `4.1.3 Status Messages`; APG modal focus / Escape / return. Проверить VoiceOver + iOS Safari, Android, реальные экранные клавиатуры и zoom 200% отдельно: **NOT_CHECKED**.

## 9. Реально проведённая QA и ограничения

**Sandbox Chromium, 2026-11-03:** комбинации ширин 1440/768/390/320 × LV/RU × DAY/NIGHT — 16 проверок, 0 X-overflow, 0 обнаруженных page JS errors, нижняя цена в viewport. DEMO сценарий 89500→91300→93900→94850; выбор unpriced опции сохраняет DEMO subtotal и показывает предупреждение. Dialog: открылся, bar скрыт под backdrop, начальный фокус в поле имени; закрытие возвращает интерфейс. Локальный sandbox не получал remote image bytes — его PNG **не используются как итоговые макеты**.

**Отдельный Firecrawl Chromium с реальными сетевыми ассетами, 2026-11-03:** AA загрузился с naturalWidth 1678, BB — с naturalWidth 1679. Сняты 4 реальные полностраничные UI-фотосборки (ссылки в §1). Проверены четыре сочетания `theme×scene` на 390px, сумма 89500 не менялась, X-overflow отсутствовал. Проверено: кнопка возврата появляется при настройке и после нажатия stage находится примерно на 85px от верха viewport, кнопка расположена над ценовым баром.

**Не проверено:** Safari iOS/Android hardware, реальная мобильная клавиатура, screen reader, объективный пользовательский B2B task-test, коммерческая лицензия исходных фото, полный contrast measurement, системные reduced-motion browser differences; external browser page cannot prove absence of all accessibility defects.

## 10. Frontend handoff / acceptance

**Следующий исполнитель:** Frontend Engineer, **не начинать реализацию до owner UX/UI review**. Создать самостоятельную `feature/*` ветку и Draft PR от согласованного baseline после сверки HEAD SHA. Не переносить экспериментальный HTML напрямую как production; использовать его как утверждаемый контракт сцены, секций, состояний и токенов. Данные и визуализации должны наследоваться из оригинальных `prototype/assets/*`, не через внешний URL и без утраты лицензий/источников.

**Acceptance gate (до Render):**
- FE-01 четыре screenshot сравнения DAY/NIGHT × 1440/390 с актуальными AA/BB, оригинальным SVG, всеми секциями;
- FE-02 четыре независимые сочетания site theme × photo, сохранение price/options/lang и fallback/reduced motion;
- FE-03 арифметика DEMO, unknown price не равен нулю, наличие DEMO/не-оферта возле суммы, НДС/доставка/монтаж явно не посчитаны;
- FE-04 320/390/768/1440, LV/RU, scroll/sticky, 200% text zoom, real iOS viewport+keyboard, отсутствие horizontal overflow;
- FE-05 dropdown/accordion, `dialog`, Esc/Tab/focus/validation errors, синхронный локальный TXT, без сетевой отправки;
- FE-06 отдельно документировать ценовые и SKU-конфликты, статусы источников, asset-rights; не показывать непроверенные performance claims;
- FE-07 визуальное и интерактивное независимое QA с screenshot/log/HEAD SHA и явным Owner approval;
- FE-08 после QA только **отдельно разрешённый** ручной Render owner-preview deploy; `main` и production не трогать.

## 11. Owner decision log / next tasks

- **APPROVED:** art thesis The Destination / Quiet Architecture; S312-only; 2 независимых переключателя; DEMO-only math.
- **OWNER REVIEW PENDING:** дизайн страницы DAY/NIGHT, mobile return thumbnail, иерархия шести групп, микрокопирайт RU/LV, компоненты и UX handoff.
- **SUPPLIER / CLIENT PENDING:** `S312-C01..C12`, официальная комплектация и цены, права на изображения, локальные технические документы.
- **ENGINEERING NOT STARTED:** текущий файл — изолированный дизайнерский прототип, не замена live-кода.
- **RENDER/PRODUCTION UNCHANGED:** никакого автодеплоя/merge, отправки заявок, реальной оплаты или CRM.

**Состояние этапа:** VISUAL PROTOTYPE READY FOR OWNER REVIEW / HANDOFF DRAFT; финальное принятие дизайна и независимые device QA не выполнены.
