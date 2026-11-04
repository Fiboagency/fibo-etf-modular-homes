# ROVELLC S312 — Mobile UX/UI QA и сравнение с MyCabin

**Дата:** 2026-11-04, Europe/Riga
**Авторский этап:** UX/UI Design Director — экспертный аудит, а не пользовательское исследование или независимая WCAG-сертификация.
**Статус:** AUDIT_COMPLETE_PARTIAL_DEVICE_COVERAGE; никаких изменений кода, PR merge или Render deploy.
**Owner-preview:** https://fibo-etf-atelier-owner-preview.onrender.com/
**Текущий Render LIVE commit:** `f4a987e04f0d468d2f5e3015d541b9fe69ecebaa` (PR #39).
**Бенчмарк:** https://www.mycabin.lv/konfigurators?model=living-100&market=LV
**GitHub source:** `prototype/index.html` и `prototype/future-living.css` на ветке `feature/etf-architectural-atelier-ui-20261101`.

## 1. Область и доказательства

Живые страницы проверялись в Chromium браузерной эмуляцией мобильного viewport через Firecrawl interactive browser. В основном использован 390x844; дополнительно проверены 375x667, 320x568, 430x932 и 390x680. Существуют фактические снимки initial, intermediate material scroll и 320px short-screen, но временные ссылки Firecrawl на изображения не прикладываются к публичному репозиторию. Real-device iOS Safari/Android, системная клавиатура, 200% text zoom, screen reader, LCP/CLS, independent security/accessibility audit: NOT_CHECKED.

Сверены HTML/CSS исходники на GitHub и статус Render `live`. Подсчёты и проверки ниже основаны на фактических действиях в браузере, а не на предположении, что статические CSS declarations достаточны.

## 2. Проверенный путь ROVELLC — PASS в ограниченном scope

- На 390x844 фиксированная `.pricebar` находилась на `top=750`, `bottom=844`, `height=94px`; после прокруток 0/600/1200/2100/3300 px координаты pricebar не изменялись. Кнопка TXT оставалась внутри viewport. На 320x568: `height≈79px`, `bottom=568`, CTA вмещается; horizontal overflow не обнаружен (`scrollWidth=clientWidth=305`).
- На ширинах 375, 390, 430 при проверенных состояниях цена и CTA видимы. Снимки также подтвердили сохранение footer bar в середине длинного списка.
- Выбраны все 12 equipment toggles; 12/12 завершились с `aria-pressed=true`. Из трех оценённых в DEMO: heated floor +2600, electric curtains +1800, LED +950; итог `89 500 → 94 850 €` без browser pageerror. Неоценённые опции увеличивают count, но не числовую цену; появляется `+ ?`.
- Все 11 material controls в четырёх группах срабатывали как radio / `aria-checked=true`. При индивидуальном выборе визуальный ресурс и mini thumbnail обычно меняются: facade `AA/CC2/VV1`; floor `UU1/OO2/PP1`; walls `GG1/DD1/FF1`; bathroom `TT1/RR1`.
- Первый `Konstrukcija un interjers` закреплён как раскрытый `section`, четыре остальные группы — `details`. Переключение LV→RU сохраняет выбранные опции и итог, проверен refresh в той же сессии.
- Site DAY/NIGHT и scene DAY/NIGHT работают независимо: graphite exterior `CC2.webp → CC1.webp`, смена темы не меняла выбранную цену. На interior `DD1.webp` переключатель фасадной сцены скрывался.
- Price breakdown открывается кнопкой, при open фокус перемещался на `closePriceDetails`, Escape закрывал и возвращал фокус к `priceOverview`.
- Локальный download: browser зарегистрировал событие с файлом `ROVELLC_S312_Komplektacija_DEMO_ru.txt` и blob URL, но фактическая загрузка сообщена sandbox как `canceled`. Сохранение и содержимое файла: NOT_CHECKED.

Ограничение: 11 swatches *изменяли выбор*, но при быстром стресс-переключении был один случай временного несовпадения stage image/последнего выбранного материала. Одиночный повторный тест floor-oak показал верный `UU1.webp`. Не утверждать, что все visual transitions безупречны на всех скоростях.

## 3. Подтверждённые проблемы и UX-наблюдения

### P1 — короткий экран скрывает визуальную обратную связь
При 320x568 `#mobilePreview` имеет `display:none`, даже когда пользователь находится среди цветовых и интерьерных опций. Это поведение явно задано `@media(max-height:629px) and (max-width:600px){.mobile-preview{display:none!important}}`. Изображение дома ушло выше viewport, поэтому изменения материала не видны без возврата наверх. **REWORK** для ключевой задачи mobile visual configuring. Убрать полное отключение; сделать небольшой always-visible контекстный preview на короткой высоте или пользовательски раскрываемое image panel (проверить, что оно не перекроет pricebar или swatches).

### P1 — маленькое изображение при прокрутке
На 390x844 ROVELLC заменяет большую основную фотографию фиксированной мини-панелью `height≈68px`, сверху, пока материал выбирается ниже. На MyCabin при прокрутке сохраняется крупное contextual image `height≈234px` и top≈50px (наблюдалось на top и scrollY=1100); pricebar остаётся снизу `height≈113px`. ROVELLC теряет визуальную возможность подробно оценить фактуру. **UX recommendation:** адаптивное preview с режимами compact/expanded (например, 68px/150–180px), меняющее текущий контекст фото при выборе. Не копировать MyCabin макет или изображения.

### P1 — выбор фасада слишком поздно появляется на первом экране
На 390x844 первый экран занят фото, заголовком, длинным intro, summary и списком manufacturer bullet points. Первые actual swatches не видны до прокрутки, в отличие от MyCabin: цвета фасада видны в пределах стартового мобильного viewport. **UX recommendation:** убрать/свернуть три вводных технических пункта в раскрываемые «Технические данные», сократить mobile intro, начать с `Fasādes tonis`, пояснение оставить рядом и после выбора.

### P1 — подтверждённый недостаточный контраст подписи детализации цены
Mobile day `.price-expand-label` («Sastāvs») — CSS `rgb(216,228,217)` на белом `rgb(255,255,255)`, расчетный contrast ≈ **1.31:1**. Этот текст функциональный и читается очень плохо. Ожидается ≥4.5:1 для normal text согласно WCAG 2.2 SC 1.4.3, если нет применимого исключения. Поменять на семантический muted с достаточным контрастом, протестировать обе темы и focus indicator. Не заявлять WCAG full compliance.

### P2 — высокая вертикальная плотность списка материалов
На мобильном используются крупные прямоугольные карточки в двух колонках: группы с тремя вариантами занимают две строки, один вариант остаётся отдельно, остаётся пустой правый слот. Повторяется при фасаде, поле, стенах. Скроллинг `Konstrukcija un interjers` превышает ~1900px на 390px. На MyCabin альтернативные цвета вынесены в компактный ряд круглых swatches (фасад 7 вариантов в строке); контент плотнее. **Предложение:** 3 компактных материала в ряд на ширинах ≥360 с квадратной текстурой и подписью ниже; на 320 выбрать адаптивную ширину или горизонтальный snap-list, не делать слишком мелкие touch targets. Увеличенное фото оценивать в контекстном preview.

### P2 — временное несоответствие изображения при быстром переключении/скролле
Стресс-тест 11 последовательных кликов выявил, что после быстрого переключения `facade-burgundy → floor-oak` один раз `aria-checked=floor-oak`, но `.stage img.active` ещё показывал `VV1.webp`. При одиночной повторной проверке и ожидании stage корректно показывал `UU1.webp`. Дальнейший keyboard-arrow стресс-тест также показал временное расхождение выбранного материала и сцены. Код `detectActiveFinish()` и `render()` оба меняют `state.visual` при scroll + click, возможна гонка. **Needs reproducible FE QA**, не считать постоянно воспроизводимым дефектом без отдельного теста на физическом устройстве. Предложение: кратковременный приоритет user click over scroll observer, измерить переходы и проверить gap behavior.

### P2 — честность/готовность цены к продаже
На ROVELLC цена DEMO `89 500 € + ?` не включает неподтвержденные отделки, НДС, доставку и монтаж. MyCabin показывает priced packages, inclusion rules, общий итог `Kopējā cena (ar PVN)` и quote-request path. Это продуктовый scope gap, НЕ UI defect прототипа. Для client MVP нужны утвержденные price rules/conditional options/VAT и отправка заявки, а не только TXT.

### P3 — подписи и микро-копирайт
4 одинаковые подписи «Materiāla vizualizācija · nestandarta variantu cena jāprecizē» повторяются над материалами; лучше один раз указать ограничение рядом с общей ценой и оставить в группах краткую техническую информацию. В мобильном pricebar цена/«+ ?» и надпись DEMO требуют более явного и читаемого контекста.

## 4. Сравнение UX по задачам

| Задача | ROVELLC owner preview | MyCabin Living 100 | Вывод |
|---|---|---|---|
| Первичный выбор фасада | ниже первого экрана | visible в первом viewport | MyCabin быстрее выводит к действию |
| Фотография при прокрутке | маленький 68px thumb; hidden на ≤629px высоты | контекстная крупная ~234px top preview | главное отставание ROVELLC |
| Образцы | высокодетализированные текстуры 2-col | компактные circular swatches | качество фото ROVELLC сильное, плотность MyCabin удобнее |
| Итоговая цена | fixed 79–94px; DEMO и unknown | fixed ~113px; с НДС | фиксация сравнима, информативность цены MyCabin выше |
| Состояния выбора | 11 swatches + 12 toggles | модель/комплектация/пол/стены/планировка/услуги | не сравнивать полный scope как реализованное требование |
| Коммерческий результат | TXT local download | quote request form | production-этап ROVELLC ещё не выполнен |
| Горизонтальный overflow на 390 | не наблюдался | небольшой ~2px | преимущество ROVELLC по reflow в этом тесте |

## 5. Рекомендуемый пакет задач и приёмка

**TASK:** `S312-MOBILE-VISUAL-CONFIG-QA-20261104`
**Status:** `PROPOSED` (не одобрено на реализацию)
**Owner:** Fibo Agency
**Handoff:** UX/UI → Frontend → QA
**Design revision:** existing approved ROVELLC Soft-Tech Product Gallery / Quiet Architecture; менять только нужный mobile configurator workflow.

Приоритет:
1. P1: не скрывать контекстное изображение на высоте ≤629; обеспечить real preview для фасада/пола/стен/плитки. Не мешать постоянной цене и не вводить конкурирующие sticky rails.
2. P1: сократить путь до первого фасада, переместив три технических bullet points из основного mobile selection flow в help/details.
3. P1: исправить contrast «Sastāvs», проверить caption и focus в day/night.
4. P2: уплотнить мобильные swatches без потери понимания текстуры/подписи; проверить сенсорный размер.
5. P2: воспроизвести и решить scroll/click image race с реальными быстрыми действиями, клавиатурой и переходами между группами.
6. Product scope: после согласования клиентом отдельно подготовить реальную цену (НДС и неизвестные доплаты), понятную quote CTA и отправку конфигурации.

**Acceptance:** 320x568, 375x667, 390x844, 430x932, 768 tablet; LV/RU; day/night theme+scene; no horizontal overflow, overlay, flicker, unresponsive controls; 11 material states, 12 equipment states; price pinned while interacting/scrolling and after reload; unknown subtotal unchanged; focus on controls not obstructed; local TXT downloaded on real phone. Записать реальные browser screenshots и test logs; physical iOS Safari/Android и 200% zoom как отдельный QA gate. Никакого изменения production до отдельного owner approval.

**Design decision:** предложения не утверждены владельцем и не являются требованием клиента SIA ETF. Замечания и сравнение с MyCabin не дают лицензии копировать чужие ресурсы.
