---
name: tuinmaximaal-asset-path
description: Determines the correct /media/wysiwyg/tm/ upload path and filename for a CMS or content asset (image, icon, logo, PDF) on the multi-store Magento site, and validates or corrects an existing asset path. Use when the user asks where to upload or store an image/asset, which media path to use, whether a media path is correct, or mentions /media/wysiwyg/tm paths. Not for Magento product gallery images.
---

Recommend the upload path + filename for a content asset under `/media/wysiwyg/tm/`, or validate one that already exists. This covers CMS and PageBuilder assets only — **not** the Magento product media gallery.

Paths and filenames are typed by hand by content editors; nothing in Magento validates them. This convention is the only thing keeping them consistent, so apply it exactly.

## Path model

```
/media/wysiwyg/tm/<locale>/<bucket>/[<page-slug>/]<filename>
```

- **`<locale>`** — a closed set. Exactly one of:
  `global` · `nl-nl` · `be-nl` · `be-fr` · `de-de` · `en-gb`
  `global` = the identical asset for every store view. Any other value is invalid.
- **`<bucket>`** — reusable assets sit in a type bucket; one-off page assets sit in `pages/`:
  - `images/` — photos, illustrations reused across pages
  - `icons/` — UI SVGs (checkmark, chevron)
  - `logos/` — brand and partner logos
  - `documents/` — PDFs
  - `pages/<page-slug>/` — an asset used on one specific page only
- **`<filename>`** — `lowercase-kebab-case`, ASCII only, no spaces, no accents/umlauts. Brand prefix (`tuinmaximaal-`) **only** on customer-facing or downloadable assets (photos, logos, PDFs); never on UI chrome (icons).

Folder and file names are always English and semantic. Language is carried by the `<locale>` segment and the asset's content — never by folder words.

## Deriving a path

Work these in order. Each is a distinct axis; infer what the description makes obvious, ask when it does not, and state every assumption in the output.

1. **Locale.** Is it the same asset for all store views, or market/language-specific? Same everywhere → `global`. Contains translated text, prices, or a market-only claim → the matching locale segment. **This is the axis descriptions most often leave silent — ask when it is not obvious.**
2. **Bucket.** Reused across multiple pages → the type bucket (`images`/`icons`/`logos`/`documents`). Bound to one specific page → `pages/<page-slug>/`, where the slug is that page's URL key.
3. **Filename.** Apply the kebab-case + brand-prefix rule above.

Completion criterion: the output names a single valid `<locale>`, one bucket (with a slug if `pages/`), and a rule-compliant filename — with each axis either inferred from the description or answered by the user.

## Output

Return both forms and a one-line rationale:

```
Upload to:   /media/wysiwyg/tm/global/pages/customer-service/tuinmaximaal-customer-service-team.jpg
Config form: wysiwyg/tm/global/pages/customer-service/tuinmaximaal-customer-service-team.jpg
Why: global (same photo all store views) · page-bound → pages/customer-service · customer-facing photo → brand prefix
```

The `Config form` (media-relative, no leading `/media/`) is what `config.xml` and code store; the URL form is what editors paste into CMS/PageBuilder.

## Validating an existing path

Given a path, run the same three axes against it and report the first rule it breaks, with the corrected path:

- `<locale>` outside the closed set (e.g. a stray `fr-fr`) → invalid.
- A globally-identical asset filed under a locale segment → should be `global`.
- Page-bound asset in a type bucket, or a reusable asset buried under `pages/` → wrong bucket.
- Filename with uppercase, spaces, accents, or a brand prefix on a UI icon → fix per the filename rule.

Legacy Dutch-named trees (e.g. `tm/nl-nl/afbeeldingen/...`) predate this convention. Flag them when asked to validate, but they are migrated deliberately, not automatically.
