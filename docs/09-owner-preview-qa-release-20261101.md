# ETF owner-preview — implementation and QA evidence

Date: 2026-11-01. Scope: presentation-only preview at https://fibo-etf-atelier-owner-preview.onrender.com/.
Approved spec: [08-approved-content-and-prototype-spec-20261101.md](08-approved-content-and-prototype-spec-20261101.md).
Current implemented branch: `feature/etf-architectural-atelier-ui-20261101`. Never merge to `main` without explicit independent approval.
Render target only: `fibo-etf-atelier-owner-preview` / `srv-dbj7148473hc73bb1k7g`. Auto-deploy disabled; deployments manually triggered.

## Delivery phases

1. Content cleanup: `9a82795ddee7bbdfa2cc8608bd56f60b2f6eef14`; deploy `dep-dbje51fb9u1s73dp7qv0`, live.
2. Persistence, reset, summary and form checks: `85b036107daf3075a42d2e40a1fd9ceb4ac015e0` (included in later live deploy).
3. LV/RU + documents: `eabb6ace33bac087ce6cfeebd0f68e1dac5d8863`; deploy `dep-dbje78nb9u1s73dpdhcg`, live.
4. Keyboard tabs, localization refinements and accessibility follow-up: `c49c14a879ced80e314eee1307a5eb96acdfc049`; deploy `dep-dbjebjp42hec73cp83bg`, live. The last source code change removes stale outer image ARIA labels and uses linked tabpanels.

## Passed checks (observed)

- Source compiled as valid JavaScript for the inline configurator and i18n layer.
- Browser starts in Latvian; switching LV→RU and RU→LV updates the displayed H1 and controls.
- Default configuration is 80 m² / anthracite / oak / white marble + black tile / Comfort / heat pump / 1 roof window / no terrace / standard layout, total **108000 EUR**.
- Grey floor = **108450 EUR**; cherry = **108650 EUR**; light oak = **108350 EUR** from default.
- Choosing grey floor → LV → page reload retains **108450 EUR** and the grey selection. Reset restores **108000 EUR** and oak.
- Natural timber + night shows image `assets/images/B.webp`.
- Cherry floor, warm taupe bath, 3 roof windows and terrace gives **116400 EUR** in observed browser interaction; + button disabled at max 3.
- Demo form rejects blank name and invalid email with precise Latvian errors, then downloads a local `.txt` file and displays successful no-send message.
- Browser keyboard ArrowRight from façade tab selects interior tab; no JS error detected in tested interaction.
- Live site HTTP 200; fresh rendered LV text shows no Russian words; units m² localized. Fresh raw HTML contains `<meta name="robots" content="noindex, follow">`.
- Latest raw HTML shows three linked `role="tabpanel"` scene containers and translated Latvian brand accessibility label. Raw HTML is considered stronger evidence for these two latest fixes than a stale browser snapshot.
- GitHub `main` remained at `83928020878339419663fc709f04ce484e4991d1` when checked; no changes to other services were requested or performed.

## QA still requiring independent manual sign-off

- Full visual layout and overflow review across desktop, tablet and mobile after final LV copy and latest patch. Earlier owner-preview mobile screenshots existed, but not an exhaustive final-regression suite.
- Full color-contrast measurements for all states and photo overlays; focus-visible and screen-reader behavior on representative assistive technologies. This is NOT a WCAG 2.2 AA certification.
- Verify downloaded RU/LV files in a local text editor, including every option label, prices and absence of PII in the direct download. Browser confirmed local download and error/success flow; complete file-content inspection was not performed.
- Keyboard and mobile tests of all possible combinations; only representative flows passed.
- Latest additional ARIA patch was confirmed in fresh raw HTML, but a subsequent browser automation attempt timed out; rerun assistive-technology test independently.

## Release restrictions

- SIA ETF has NOT approved real prices, modules, commercial terms or final branding. Current data is invented for demonstration.
- All 10 supplied AI visuals approved by the Fibo Agency owner for presentation to SIA ETF only.
- No backend, payment, lead transmission, database storage or persistence of form name/email.
- Owner-preview is public by URL but requests nonindexing; `noindex` is not access control.
