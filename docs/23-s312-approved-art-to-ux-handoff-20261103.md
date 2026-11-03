# ROVELLC S312 — зафиксированное направление и handoff UX/UI / frontend
**Дата:** 2026-11-03 · **Статус:** ART DIRECTION APPROVED IN CHAT / IMPLEMENTATION NOT STARTED · **Task:** ETF-ROVELLC-S312-VISUAL-20261103

## 0. Решение владельца и границы
- В текущем диалоге владелец Fibo Agency сообщил «утвердил» в ответ на представленную концепцию [PR #20](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/20) / демонстрационное HTML-превью DAY/NIGHT. **PR #20 проверен: merged**; изменена только документация в `feature/etf-architectural-atelier-ui-20261101`.
- **Зафиксированное визуальное направление:** `The Destination / Quiet Architecture`; DAY = `Architectural Nature`; NIGHT = `Architectural Experience`. Это утверждение художественного направления, **не** утверждение коммерческой оферты, данных производителя, реальных цен, лицензий, новой архитектуры backend или деплоя.
- **Версия артефакта:** `ROVELLC_S312_DAY_NIGHT_art_preview.html`, SHA256 `574d305604d7439742e2712fa8a9f010df99d537710956f24123e00a5ed66592`, отдельный файл в текущем диалоге ChatGPT, **не расположен в GitHub**. Этот файл — экспериментальный браузерный концепт с верхней панелью просмотра, не готовый production-HTML. При передаче проверять хеш предоставленного локального файла. Нельзя выдавать URL sandbox за долгоживущий публичный адрес.
- **Источник художественной спецификации:** [docs/22](22-s312-digital-art-direction-proposal-20261103.md); UX-конфигурационная детализация: [pending PR #19](https://github.com/Fiboagency/fibo-etf-modular-homes/pull/19) (`docs/20`, `docs/21`, ещё Draft), факты и конфликты: [docs/17](17-rovellc-business-brand-marketing-audit-20261103.md), [docs/18](18-s312-technical-dossier-and-conflicts-20261103.md), [docs/19](19-rovellc-s312-cross-role-handoff-20261103.md), [data/s312-source-data](../data/s312-source-data-20261103.json).
- **Актуальная опорная ветка перед этим handoff:** `feature/etf-architectural-atelier-ui-20261101` commit `2f0343e24d149be164a0bdc1730cce29fc8c303d`; перепроверить HEAD в день создания code-PR. Открыть отдельную feature-ветку для UI реализации; не менять `main`.
- **Основная текущая версия для просмотра:** `fibo-etf-atelier-owner-preview.onrender.com`, Render service `srv-dbj7148473hc73bb1k7g` / workspace `tea-dba7n2gm7kps73fq8j30`, ручной деплой; PR-документация не означает обновлённую публикацию.

## 1. UX-цель после approval
Сделать из нынешнего демонстрационного конфигуратора **визуально убедительную архитектурную продуктовую страницу** только одной модели S312. Первый B2B-посетитель (глэмпинг/бутик-отель/туристическая локация — маркетинговая гипотеза) должен за несколько секунд увидеть *архитектурный объект*, затем найти факты, план, оснащение, прозрачный демонстрационный итог и честный способ сохранить локальную конфигурацию.

**Изменение относительно текущего продукта:** не косметическое перекрашивание конфигуратора, а продуманная page narrative: контекст размещения → архитектурный hero → подтверждённая карточка S312 → схема и варианты → всегда видимая стоимость → проектное объяснение. Без обещания доходности, окупаемости, «без разрешений», климата или гарантий.

## 2. Точный front-end scope
| Region | UX/UI & art contract | Protected invariant |
| --- | --- | --- |
| Brand header | логотип ROVELLC SVG, компактный продуктовый идентификатор, LV/RU, отдельные иконки theme | не допускать замены логотипа / синих системных emoji |
| Hero + stage | крупная S312 AA/BB, архитектурный слоган только как approved creative direction, максимальная читаемость формы | не перерисовывать геометрию S312; не обрезать нос/крышу/опоры |
| Product facts | 38 m² **covered** (ссылка на каталог), 11.5×3.3m, одна спальня/гостиная/санузел/балкон | спорные height / guests скрыты или явно помечены SOURCE_CONFLICT |
| Plan | существующий schematic SVG с предупреждением, что это не инженерный чертёж | не объявлять схему рабочей документацией |
| S312 Config | одна модель; ясные переключатели с 6 статусами; опции группируются по задачам, не имитируют каталог других SKU | не добавлять 18 моделей и выдуманные размеры |
| Price bar | постоянная снизу сумма **DEMO**, суммы меняются без задержки, всегда виден CTA | не выдавать демо-цену за реальную, сохранить safe-area/keyboard |
| Request modal | локальная генерация .txt и понятное объяснение «ничего не отправляется» | backend, email, CRM, PII-отправка вне текущего scope |
| Story/footer | композиционная «архитектура + условия проектного расчёта», Fibo credit в подвале | не выдумывать кейсы/цифры/документы |

**Файлы исходного prototype:** `prototype/index.html`, `prototype/theme.css`, `prototype/assets/images/AA.webp`, `BB.webp`, `prototype/assets/brand/logo.svg`, `prototype/assets/s312-layout-schematic.svg`. Визуальный preview-HTML нужно адаптировать; убрать из пользовательского сайта review toolbar и desktop/mobile симулятор, заменить удалённые URL на существующие локальные asset paths. Файл концепции **не копировать в репозиторий напрямую** без аудита логики, текстов и прав.

## 3. Защищённые состояния и поведение
- Два независимых управления: **site theme** (DAY UI/NIGHT UI) и **photo scene** (AA/BB). Все четыре комбинации обязаны выглядеть корректно. Смена темы **не** меняет фото, язык, выбранные опции, цену; смена сцены **не** меняет сайт или цену.
- View Transition circular reveal от иконки темы **680ms**, fallback **580ms**, `prefers-reduced-motion` = без анимации. Не терять эту функцию при изменении CSS/DOM.
- Смена фото — мягкий переход, но не смена неподтверждённого фасада/интерьера от электрических опций.
- `LV` по умолчанию, `RU` как второй язык owner-preview; будущие `EN/LT/ET` без ложных готовых переводов. Не ломать сохраняемую locale/theme/scene/option state; в хранилище не писать персональные данные формы.
- Демонстрационный baseline **89 500 €** + «шторы» **1 800 €**, «подогрев пола» **2 600 €**, «дополнительная LED» **950 €**. При трёх включённых учебных опциях получается **94 850 €**. Все числа — `DEMO_ONLY`, реальные цены в `data/s312-source-data-20261103.json` остаются `null`.
- «Дополнительная LED» **не подтверждена как реально платная SKU-опция**; маркировать учебной, не утверждать комплектацию как commercial BOM.
- Состояния компонента: `included_confirmed`, `optional_priced_confirmed`, `optional_price_unknown`, `source_conflict`, `unsupported`, `demo_only`. Не показывать `+0€` как ответ на unknown price; при неопределённом прайсе `quote_on_request`.
- Текущие CTA только `download configuration .txt` и `view local demo request`; никакой отправки на сервер/псевдо-подтверждения получения.

## 4. Страницы, адаптивность, дизайн-токены
- **Desktop 1440:** двухколоночная композиция архитектурной сцены ~65–69% + конфигуратор; блок доказательных характеристик и схемы, отдельная нижняя editorial секция; вся страница от шапки до диалога и подвала имеет DAY и NIGHT состояния.
- **Tablet 768:** сложить stage и configurator, не вытягивать изображение с неверным crop.
- **Mobile 390:** цельный вид дома; внутри сцены фото-переключатель; компактный header; 2–3 читаемых характеристики без ложной высоты/occupancy; опции ниже; закреплённая цена и CTA; возможность возврата к дому. Отдельное floating thumbnail — только при подтверждении UX-тестом; не закреплять большую фотографию над sticky bar.
- **320:** отсутствие горизонтального скролла, не перекрываются модаль, клавиатура и sticky bar; safe-area для iPhone.
- **Типографика:** editorial serif в hero, компактный sans для технических элементов; до кода проверить лицензии выбранных шрифтов и реальные RU/LV глифы `ā č ē ģ ī ķ ļ ņ š ū ž`, `ё й ъ ы щ`.
- **Палитры:** точные кандидатные токены `bg/surface/elevated/text/border/accent/CTA/price` в [docs/22 §5](22-s312-digital-art-direction-proposal-20261103.md). Подтверждены как визуальное направление, **не** как финальная численно проверенная дизайн-система; проверить контрасты реальных компонентов, focus, error, disabled в обеих темах.
- **Ассеты:** AA/BB, logo.svg, schematic.svg — уже используются в owner-preview; публичное переиспользование, права на визуализации/марку и исходники по иным продуктам `UNKNOWN`. Не добавлять каталог PDF/изображения производителя в публичный GitHub.

## 5. UX delivery package
1. Реальный desktop keyframe **1440px** и mobile **390px** для DAY и NIGHT (4 композиции) на **загруженных AA/BB**, а не только CSS на пустом блоке.
2. Responsive annotations **320px** и **768px**, crop/focal-point для 320/390/768/1440.
3. Таблица компонентов с состояниями `default/selected/unknown/conflict/disabled/focus/hover/error`; modal, sticky price, раскрытый план.
4. Интерактивная/тестируемая UI спецификация state `theme×scene×locale×options×priceMode×modal`, включая refresh/local storage.
5. Полный asset manifest и source/rights статус; не подменять фотографии выдуманным интерьером.
6. QA матрица с фактическими screenshots DAY/NIGHT × mobile/desktop, ручной кроссбраузерной проверкой iOS Safari, keyboard, reduced motion, contrast, overflow, price math.
7. Отдельный code-PR после design-to-code handoff и проверки продукта. Существующие `docs/20`/`docs/21` в Draft PR #19 содержат расширенный UX чек-лист; не объявлять их merge или owner-approved scope без реального статуса GitHub.

## 6. Решения и блокеры
**Approved:** artistic direction as above; house=S312 only; paired DAY/NIGHT site treatment; distinct stage photos; demo pricing retained only with disclaimers.

**Still NOT approved / requires product or owner confirmation:** supplier-approved S312 SKU revision, height 3.35 vs 3.15m, occupancy 3–5 vs 2–3, BOM, compatibility, prices, VAT, transport/installation, rights for reuse of visual assets, local certifications and lead backend/CRM. The `S312-C01..C12` conflicts remain unresolved; art approval does not convert them into facts.

**Release gating:** next verified implementation must be a separate `feature/*` branch and Draft PR, with browser screenshots and functional evidence tied to that exact HEAD SHA. The owner later reviews a **specific preview commit**, then separately permits manual Render owner-preview deploy. Nothing in this document authorizes production or `main` changes, auto-merge, client correspondence or paid services.

## 7. Stage status
- Art direction: `APPROVED_BY_OWNER_IN_CHAT`; PR #20 `MERGED`.
- UX/UI: `HANDOFF_DRAFT_READY` (this document); actual UX keyframes and device interaction QA `NOT COMPLETED`.
- Supplier data: `OPEN_CONFLICTS` (docs/18, JSON).
- Frontend implementation: `NOT STARTED` in this step.
- Production + Render: `UNCHANGED`; any deploy requires separate owner review.
