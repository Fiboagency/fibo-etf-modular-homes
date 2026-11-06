# Internal contract review / Fibo Agency

This directory contains a **generic, static, local-first review tool**. It intentionally does **not** contain the ETF/ROVELLC contract, its annexes, prices, payment terms, contact information, or any review comments.

## Workflow

1. Download `index.html` and open it in a modern browser, or use the same generic page on a trusted hosting origin.
2. Load a **private** contract-data JSON with `docId`, `sections`, `items`.
3. Review individual clauses using mutually exclusive **Agree** / **Disagree** checkboxes and optional comments.
4. Save the complete review as JSON and a list of disagreements as Markdown. Store both privately.
5. Re-import the review JSON to continue in the same document version.

The review JSON is local to the reviewer. Review progress is additionally stored in browser `localStorage` (origin-specific, no accounts or synchronization). Browser storage may be unavailable, cleared or read by other scripts on the same origin; downloading the review JSON is essential. For sensitive work, prefer the separately provided **self-contained offline HTML** over public-hosted use.

**Security:** Never add contract-data JSON, exported review files, customer contact data or internal commercial terms to a public branch, pull request, GitHub Issue or GitHub Pages. The HTML contains no analytics, CDN, external scripts or form submissions.

## Contract-data schema

```json
{
  "schemaVersion": 1,
  "docId": "example-private-v1",
  "title": "Internal agreement review",
  "subtitle": "Draft",
  "notice": "Working copy only",
  "source": "private document",
  "sections": [
    {"id": "s1", "title": "1. Section name", "part": "Agreement"}
  ],
  "items": [
    {"id": "1.1", "section": "s1", "label": "Clause 1.1", "text": "Clause text", "page": 1, "tags": []}
  ]
}
```

The content of additional annexes that were not provided must be imported separately; do not fabricate legal text. Checkbox decisions and exported comments are work-in-progress notes, not legal acceptance or an electronic signature.
