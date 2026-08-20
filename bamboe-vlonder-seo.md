# SEO — "Bamboe vlonder" homepage block

Optimization of the image `alt`/`title` for the "Bamboe vlonder" block on the homepage,
across all 6 staging environments. The block links through to a landing page (see **Links to**).

**Current state (all environments):** the block uses one shared image
`/media/wysiwyg/tm/nl-nl/afbeeldingen/Home/ACC-30001-0001_03.jpg` with `alt="ACC-30001-0001_03"`
(raw SKU) and an empty `title`.

**Image content:** a dark-brown bamboo decking terrace, raised with wide steps, a white garden
lounge set, a cream parasol, hedge and planters.

---

## Recommended values

### NL — https://tuinmaximaalnl.intern.systems/
- **Links to:** `/bamboe-vlonder`
- **Filename:** `bamboe-vlonder-tuinterras.jpg`
- **alt:** `Bamboe vlonder als verhoogd tuinterras met loungeset en parasol`
- **title:** `Duurzame bamboe vlonder voor in de tuin`

### BE (nl) — https://tuinmaximaalbe.intern.systems/
- **Links to:** `/bamboe-vlonder`
- **Filename:** `bamboe-vlonder-tuinterras.jpg`
- **alt:** `Bamboe vlonder als verhoogd tuinterras met loungeset en parasol`
- **title:** `Duurzame bamboe vlonder voor in de tuin`

### BE (fr) — https://tuinmaximaalbe.intern.systems/fr/
- **Links to:** `./terrasse-en-bambou`
- **Filename:** `terrasse-en-bambou-jardin.jpg`
- **alt:** `Terrasse en bambou surélevée avec salon de jardin et parasol`
- **title:** `Terrasse en bambou durable pour le jardin`

### FR — https://tuinmaximaalfr.intern.systems/
- **Links to:** `./terrasse-en-bambou`
- **Filename:** `terrasse-en-bambou-jardin.jpg`
- **alt:** `Terrasse en bambou surélevée avec salon de jardin et parasol`
- **title:** `Terrasse en bambou durable pour le jardin`

### DE — https://tuinmaximaalde.intern.systems/
- **Links to:** `/boeden-bambus`
- **Filename:** `bambus-terrassendielen-garten.jpg`
- **alt:** `Bambus-Terrassendielen als Gartenterrasse mit Loungemöbeln und Sonnenschirm`
- **title:** `Langlebige Bambus-Terrassendielen für den Garten`

### UK — https://tuinmaximaaluk.intern.systems/
- **Links to:** `/bamboo-decking`
- **Filename:** `bamboo-decking-garden-terrace.jpg`
- **alt:** `Raised bamboo decking terrace with garden lounge set and parasol`
- **title:** `Durable bamboo decking for your garden`

---

## Quick-reference table

| Env | Filename | alt | title |
|-----|----------|-----|-------|
| NL | `bamboe-vlonder-tuinterras.jpg` | Bamboe vlonder als verhoogd tuinterras met loungeset en parasol | Duurzame bamboe vlonder voor in de tuin |
| BE-nl | `bamboe-vlonder-tuinterras.jpg` | Bamboe vlonder als verhoogd tuinterras met loungeset en parasol | Duurzame bamboe vlonder voor in de tuin |
| BE-fr | `terrasse-en-bambou-jardin.jpg` | Terrasse en bambou surélevée avec salon de jardin et parasol | Terrasse en bambou durable pour le jardin |
| FR | `terrasse-en-bambou-jardin.jpg` | Terrasse en bambou surélevée avec salon de jardin et parasol | Terrasse en bambou durable pour le jardin |
| DE | `bambus-terrassendielen-garten.jpg` | Bambus-Terrassendielen als Gartenterrasse mit Loungemöbeln und Sonnenschirm | Langlebige Bambus-Terrassendielen für den Garten |
| UK | `bamboo-decking-garden-terrace.jpg` | Raised bamboo decking terrace with garden lounge set and parasol | Durable bamboo decking for your garden |

---

## CTA buttons

The block's link currently uses generic anchor text ("Lees meer / Read more"), which is weak for
SEO (no keyword) and accessibility (many identical links on the page). The fix is **concise,
keyword-bearing button text** — not a link `title`. The link `title` attribute is not an SEO
ranking factor and is usually ignored, so it is intentionally omitted below.

| Env | Current text | Recommended button text (concise) |
|-----|--------------|-----------------------------------|
| NL | Lees meer | Bekijk bamboe vlonders |
| BE-nl | Lees meer | Bekijk bamboe vlonders |
| BE-fr | Lire la suite | Voir les terrasses en bambou |
| FR | Lire la suite | Voir les terrasses en bambou |
| DE | Mehr lesen | Terrassendielen ansehen |
| UK | Read more | View bamboo decking |

**Fallback only:** if the design must keep the short generic label ("Lees meer / Read more"),
leave the visible text as-is and add an `aria-label` describing the destination
(e.g. NL `Bekijk bamboe vlonders`, UK `View bamboo decking`). Use `aria-label`, not `title` —
it is the correct accessibility tool. Note this fallback helps screen readers, not SEO.

## Extra: "Inspiration" blog block (DE) — missing alt/title

Separate homepage block (heading "Inspiration", links to `/blog`, image `inspiration.jpg`).
On DE the `alt` is just the filename (`inspiration`) and the `title` is empty. NL already has
proper copy; below is the DE translation in the formal register.

- **NL reference — alt:** `Familie geniet van een gezellige maaltijd onder de terrasoverkapping.`
- **NL reference — title:** `Lees inspirerende blogs over het optimaal genieten van je terrasoverkapping.`

**DE — recommended:**
- **alt:** `Familie genießt eine gemütliche Mahlzeit unter der Terrassenüberdachung.`
- **title:** `Lesen Sie inspirierende Blogs, wie Sie Ihre Terrassenüberdachung optimal genießen.`

## Notes

- **Shared image file:** all sites currently reference the same file in the `nl-nl` media folder.
  Renaming is optional and a larger job (re-upload + update every reference). If the file stays
  shared, use `bamboe-vlonder-tuinterras.jpg` as the single filename; the localized `alt`/`title`
  are still set per site in the PageBuilder element, so they can differ even with one shared file.
- **`alt` vs `title`:** `alt` describes the image (accessibility + image SEO); `title` is the
  benefit-led hover caption. Keywords match each site's heading and landing-page slug.
- **Keep it concise:** all `alt` values are kept under ~65 characters and avoid keyword stuffing.
