# Scope clarification — 2026-11-02

**Status:** incoming requirements analysed; implementation and estimate not yet approved.  
**Source materials:** private product catalogue and client correspondence are intentionally not copied into this public repository.

## New information to incorporate into discovery

- Client has positively confirmed that the existing interactive prototype reflects the desired visual direction.
- Target catalogue: six house series, provisionally eighteen selectable model/size entries.
- The supplied catalogue includes eighteen distinct model codes across the six series, but the series do **not** each have three listed codes. A balcony configuration also appears as a variation of an existing code. The final production model matrix must be supplied/approved before importing catalogue data.
- Add selectable equipment to each eligible model (e.g. underfloor heating and electric curtains), immediately reflected in the calculated total.
- The current total must remain continuously visible in a bottom-anchored summary bar throughout configuration, on mobile and desktop, with a clear path to a quote request.
- mycabin.lv is a functional/visual benchmark, **not** a requirement to copy its site or implement every feature.
- Previous discovery assumptions still need confirmation: five locales (LV, EN, LT, ET, RU), custom application, model/options/price administration, quote request by email, no payment or automated invoice.

## Proposed MVP behaviour (pending acceptance)

1. Series -> model/size -> configurable options -> review -> quote request.
2. Price is calculated from the selected model's base price and allowed option prices; refresh without a page reload.
3. Total and selected additions are clearly labelled; VAT, inclusions/exclusions, and any starting-price disclaimer are supplied by the business owner.
4. Bottom pricing bar stays visible without hiding mobile content or conflicting with the keyboard/cookie consent.
5. Admin can enable/disable models and allowed options, update base/add-on prices, and change marketing content without code deployment.
6. Submitted enquiry includes the model identifier, chosen options, price snapshot, locale and user contact details, delivered only via approved private channels.
7. Price calculation and form submission require responsive and locale-specific QA.

## Open questions blocking a fixed quotation

- Confirm the exact eighteen production model IDs and treatment of non-standard catalogue variants.
- Supply a structured base-price table and equipment price/compatibility matrix per model; define discounts, VAT policy, and delivery/installation inclusion.
- Specify the full list of configurable options, dependencies and mutually exclusive combinations.
- Decide whether changing a choice must also change imagery, and supply the allowed image/3D assets and usage permissions.
- Clarify who owns the product brand/content rights and which manufacturer claims may be published.
- Confirm the approved five-language source texts, technical translations, and who signs off each locale.
- Confirm quote recipients, required fields, spam protection, data-retention/privacy requirements and consent text.
- Confirm admin user roles, integrations, analytics, domain/hosting ownership and launch acceptance procedure.

## Implementation approach — not yet a decision

- **2D selector:** least visual complexity, cheaper but a weaker premium configurator.
- **Pre-rendered visuals:** recommended MVP approach; option/size changes use prepared imagery. Asset production is a separate dependency and must be scoped.
- **Interactive 3D:** distinct larger scope requiring models, performance/compatibility work and a new schedule.

## Next actions

1. Agree final model and option matrix, pricing rules, asset scope and client-side text ownership.
2. Freeze MVP specification, acceptance criteria, milestone delivery plan and exclusions.
3. Prepare private cost/schedule proposal and obtain explicit approval before any external communication.
4. Once approved, create implementation branches/PRs. Production deployment requires separate approval.

## Repository housekeeping

The files `docs/01-original-inquiry-lv.md`, `docs/02-client-brief-ru.md`, `docs/03-discovery-and-scope.md` and `docs/04-next-chat-handoff.md` were not found on `main` during this review. Because this repository is **public**, do not reconstruct or commit private letters, phone numbers, catalogue PDFs, or commercial terms here.
