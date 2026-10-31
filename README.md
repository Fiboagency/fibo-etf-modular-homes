# ETF Modular Homes — project workspace

This repository is used by Fibo Agency to plan and review a modular-homes website and product configurator.

## Current stage — 2026-11-01

- Discovery and **interactive concept prototype** (non-production).
- A standalone static prototype is available for owner review: https://fibo-etf-configurator-demo.onrender.com
- The HTML demo lives in [`prototype/index.html`](prototype/index.html), with instructions at [`prototype/README.md`](prototype/README.md).
- The functional scope and **unconfirmed assumptions** are documented in [`docs/05-configurator-prototype-scope.md`](docs/05-configurator-prototype-scope.md).
- The prototype uses fictional prices, hypothetical house sizes and original schematic SVG illustrations. It is not a quote or production implementation.
- No production code or customer data has been deployed. All changes are created in feature branches and reviewed via pull requests.

## Target MVP (to be confirmed)

- Catalogue of at least six modular-house models.
- House sizes, finish and accessory options, live estimated prices.
- Quote-request workflow, product and price administration.
- Five locales: LV, EN, LT, ET, RU.
- Responsive, premium visual design.
- No online checkout or automatic invoices.

## Missing source documentation

The four expected source documents below are **not present on `main`** as of 2026-11-01:

- `docs/01-original-inquiry-lv.md`
- `docs/02-client-brief-ru.md`
- `docs/03-discovery-and-scope.md`
- `docs/04-next-chat-handoff.md`

Do not infer or reconstruct these from memory. If recovered, review privacy before committing; **do not publish client contacts, private correspondence or commercial terms in this public repository**.

## Next tasks

1. Owner reviews the interactive prototype and selects the visual direction.
2. Confirm actual house models, materials, options, pricing rules and VAT display.
3. Choose the rendering strategy: SVG/2D, pre-rendered image variants or interactive 3D.
4. Approve MVP architecture, pricing/option administration, server-side quote validation and lead handling.
5. Define acceptance tests and five-language copy requirements before production development.

## Approved visual direction (Fibo Agency internal, 2026-11-01)

The owner selected **Architectural Atelier (Direction A)** for an interactive prototype. The implementation is in the isolated `feature/etf-architectural-atelier-ui-20261101` branch; it is not a client-approved production brand, contract, product/pricing model or release.

- Design proof and history: `prototype/design-review.html`, `docs/06-premium-brand-art-direction-ru.md`
- Implemented design handoff and test matrix: `docs/07-architectural-atelier-implementation.md`
- Functional static HTML and user-provided photos: `prototype/index.html` + `prototype/assets/images`
- Important: dynamic options/values are invented demonstrations, server request delivery and back office are **not implemented**.
- Next: owner review of draft PR; approve logo/rights, actual model/material/price data and locales before real MVP.

