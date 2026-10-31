# Interactive configurator prototype — v0.1

Status: **Prototype prepared locally for internal review. Not deployed, not approved, not production-ready.**

## Goal

Validate the proposed product-selection UX before committing to a commercial estimate and full backend architecture. Create an original premium visual concept; do not copy MyCabin's source code or imagery.

## Implemented in the prototype source package

- Six fictional catalog models: ETF ONE, DUO, LOFT, FAMILY, PANORAMA, GRAND.
- Three floor-area choices per model, three specification packages, three facade colors, two frame colors, and four optional upgrades.
- Interactive architectural SVG concept plus a schematic (non-engineering) floor-plan illustration.
- Live sample-price calculation, price breakdown, constraints for some add-ons, shareable configuration and JSON export.
- Responsive interface and demonstration RU/LV/EN/LT/ET translations. Translations need native review.
- Minimal Node.js backend with `POST /api/quote` that independently validates options and recomputes the sample price; six automated pricing tests.
- Form has a **demo-only** outcome. No real customer contact data is stored and no emails are sent.

## Important limitations

- All prices, house sizes, models, options, and names are invented **demo data**, not confirmed product information.
- No PostgreSQL database, admin dashboard, sales CRM, real lead submission, production hosting, server user authentication, production security hardening, or genuine architectural 3D.
- Form asks for dummy contact details but submits only configuration for optional price verification; it does not send identity fields to the backend.
- Browser can open the self-contained HTML without any server; backend demo is distributed separately as a Node.js source archive in the chat.
- Code archive is **not yet committed** to GitHub; this PR records the stage and decisions. Upload and code review are a separate next step.

## Architecture to validate for MVP

- Next.js / TypeScript frontend, server-side API and PostgreSQL; hosting on Render after approval.
- Versioned price calculations on server, stored configuration snapshots, audit trail of admin price changes.
- Admin management of models, sizes, options, localized content and permissible dependencies.
- GDPR-compliant lead capture and securely routed notifications after approval.

## Questions for customer

1. Are sizes chosen from fixed variants or freely entered?
2. Which options change the visual appearance, and are renders available for each?
3. How do package, variant, VAT and option-dependency pricing rules work?
4. Is one admin role enough, and who supplies approved translations?
5. What data must be submitted in a quote and who receives it?

## Next tasks

1. Review UX and design direction in the interactive HTML demo.
2. Confirm target MVP and acceptance criteria against the client brief.
3. Review missing requirements, imagery and pricing rules with client.
4. Commit reviewed code to a development branch and run integration and accessibility tests.
5. Create PostgreSQL-backed admin and real lead pipeline only after scope approval.
