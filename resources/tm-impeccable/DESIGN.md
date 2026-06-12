# DESIGN — Tuinmaximaal

> The visual system for the Tuinmaximaal storefront (Magento 2 + Hyvä theme `Valantic/base`).
> Pairs with [PRODUCT.md](PRODUCT.md) (strategy: who / what / why). This file documents *what
> exists in the theme today* and how to build with it.

**Source of truth:** the Tailwind theme config and component CSS, not this file. If the two
ever disagree, the code wins and this doc should be updated.

- Tokens → [`tailwind.config.js`](app/design/frontend/Valantic/base/web/tailwind/tailwind.config.js)
- Spacing generator → [`tailwind.spacing.js`](app/design/frontend/Valantic/base/web/tailwind/tailwind.spacing.js)
- Component CSS → [`base/web/tailwind/components/`](app/design/frontend/Valantic/base/web/tailwind/components/)
- Live style guide → `Valantic_StyleGuide` (route `styleguide/index/index`)

---

## 0. Aesthetic direction

Warm, light, dependable commerce. A creamy sand/beige canvas with deep forest-green structure
and a single confident orange accent for primary actions and highlights. The feel to aim for
is **Coolblue's clarity and trust, IKEA's organization, and Hornbach's practical robustness**
(see PRODUCT.md) — large, mainstream, well-ordered retail that earns confidence through
legibility and structure, never through decoration. Generous space, strong typographic
hierarchy in Articulat CF, tasteful restraint.

- **Color strategy:** warm neutral surfaces dominate (~60%); green structure and secondary
  text (~30%); orange/lime accents stay rare (~10%).
- **Type direction:** one family (Articulat CF), hierarchy by weight + size; heavy display
  weights for headings, calm 16px body.
- **Motion energy:** low and functional. Motion confirms state; it never performs. (See §10.)
- **Theme:** light, always.

---

## 1. Color

Colors are exposed under the `tmx` namespace and as semantic role aliases. Prefer the
**role aliases** in markup; reach for raw `tmx-*` only when no role fits.

### Palette

#### Primary
| Name | Token | Hex |
|------|-------|-----|
| Dark Green | `tmx-primary-darkGreen` | `#001A13` |
| Green | `tmx-primary-green` | `#003017` |
| Medium Green | `tmx-primary-mediumGreen` | `#002E21` |
| Light Green (CTA) | `tmx-primary-lighterGreen` | `#809700` |
| Light Green Second | `tmx-primary-lighterGreenSecond` | `#8BA407` |
| Light Green Shadow (CTA hover) | `tmx-primary-lightGreen` | `#6D8005` |
| Orange (accent) | `tmx-primary-orange` | `#FF8000` |
| Yellow | `tmx-primary-yellow` | `#FFCB00` |
| Red | `tmx-primary-red` | `#FF4D4D` |
| Blue | `tmx-primary-blue` | `#80A5E4` |
| Brown | `tmx-primary-brown` | `#8A7B6C` |
| Black | `tmx-primary-black` | `#11171F` |

#### Secondary (warm surfaces)
| Name | Token | Hex |
|------|-------|-----|
| Sand | `tmx-secondary-sand` | `#F5E6D7` |
| Beige | `tmx-secondary-beige` | `#FFF5ED` |
| Bone | `tmx-secondary-bone` | `#E0D2C5` |

#### Neutral
| Name | Token | Hex |
|------|-------|-----|
| Grey | `tmx-neutral-grey` | `#636363` |
| Medium Grey | `tmx-neutral-mediumGrey` | `#878787` |
| Light Grey | `tmx-neutral-lightGrey` | `#E3E3E3` |
| Dark Grey | `tmx-neutral-darkGrey` | `#151A1F` |
| White | `tmx-neutral-white` | `#FFFFFF` |

#### Status
`status.info` blue-700 · `status.error` red-500 · `status.success` green-500 ·
`status.warning` yellow-700 (standard Tailwind shades).

### Semantic roles (use these in markup)
| Role | Default | Hover / variant |
|------|---------|-----------------|
| Body text | `text-body` → green | — |
| Link | `text-link` → green | `text-link-main` / `text-link-hover` → lime |
| Header / footer bg | `bg-header`, `bg-footer` → green | search `bg-header-search` → dark green |
| Cart count, price | `bg-header-cartCount`, `bg-price` → orange | — |
| Menu surface | `bg-menu` → sand; mobile → beige | active item → orange |
| USP bar | `bg-usps` → beige; mobile → sand | — |
| Category / breadcrumb bg | beige | — |
| Container | `bg-container` `#fafafa`; lighter `#fff`; darker `#f5f5f5`; beige | — |
| Heading highlight | `bg-heading-highlight` → orange, `text-heading-highlight` → white | — |
| Button primary | `bg-btn-primary` → lime, `text-btn-primary` → white | hover → light-green-shadow |
| Button secondary | transparent bg, `text-btn-secondary` → green, border green | hover → green bg, white text |
| Active menu / focus accent | `border-activeMenuItem` → orange | — |

---

## 2. Typography

**One family: `ArticulatCF`** (`font-body`), self-hosted TTF. Hierarchy comes from
weight + size, not a second face — do not introduce another font.

| Weight | Value |
|--------|-------|
| Regular / Normal | 400 |
| Medium | 500 |
| Demibold | 600 (`font-semibold`) |
| Bold | 700 (`font-bold`) |
| Heavy | 900 (`font-black`) |

### Heading classes
Element tags (`h1`–`h6`) already apply the matching class, so semantic HTML gets the styling
for free. Use the `.heading-N` class directly when you need the look without the level.

| Class | Size token | Size / line-height | Weight | `.heading-small` |
|-------|-----------|--------------------|--------|------------------|
| `.heading-1` | `text-9.1` | 36px / 1.31 | 900 | → `text-10` (40px) |
| `.heading-2` | `text-7.6` | 30px / 1.30 | 900 | → `text-8` (32px) |
| `.heading-3` | `text-6.1` | 24px / 1.29 | 900 | — |
| `.heading-4` | `text-5.1` | 20px / 1.30 | 700 | — |
| `.heading-5` | `text-4.4` | 18px / 1.28 | 700 | — |
| `.heading-6` | `text-4.1` | 16px / 1.31 | 600 | — |

> Note: `.heading-small` is *larger* than the base in this system (a deliberate variant used
> in specific contexts), not smaller.

**`.heading-highlight`** — orange highlight chip behind the text (white text,
`bg-heading-highlight`), rotated `-2deg`. The signature brand flourish; use sparingly on
hero/section headings.

### Paragraph & body
Base body is `text-base` (16px / 1.5), color `text-body` (green), `font-body`.

| Class | Size | Notes |
|-------|------|-------|
| `.paragraph-base` | 16px / 1.5 | Default body copy |
| `.paragraph-sm` | 12px / 1.5 | Small |
| `.paragraph-esm` | 10px / 1.5 | Extra small |
| `.paragraph-tiny` | 10px, bold, **uppercase** | Labels only — never long passages |
| `.paragraph-highlight` | orange chip, 900, rotated `-2deg` | Inline emphasis flourish |

Cap body line length around 65–75ch for readability.

### Lists
- **`.list-base`** — dash-marker list (`content-dash`), `.list-text` at 14px / line-height 24px.
- **`.list-usps`** — green check-circle marker (lime `#809700` SVG), `.list-text` at 14px.
  Used for product USPs / selling points. Reinforces the "confidence" goal — surface proof
  as scannable checks.

---

## 3. Spacing

The spacing scale is **generated** (`tailwind.spacing.js`): a token `N` equals `4 × N` px,
with `.5` half-steps adding 2px. So `p-2` = 8px, `px-3.5` = 14px, `py-4.5` = 18px,
`gap-6` = 24px. Range runs 0 → 500px.

Practical rhythm:
- **Element gap:** 8–24px (`gap-2`–`gap-6`) inside components.
- **Section gap:** 32–40px (`gap-8`–`gap-10`) between major blocks.
- Prefer `gap` on flex/grid parents over per-child margins.
- Vary spacing for hierarchy — more space above a heading reads as more important. Avoid
  uniform padding everywhere.

---

## 4. Radius, shadow, layout

### Border radius
| Token | px | Typical use |
|-------|----|-------------|
| `rounded-0.5` | 2 | hairline chips |
| `rounded-1` | 4 | **buttons** (`.btn` uses `rounded-1`), inputs (`rounded` = 4) |
| `rounded-1.5` | 6 | |
| `rounded-2` | 8 | cards |
| `rounded-2.5` | 10 | |
| `rounded-3` | 12 | larger cards |
| `rounded-3.5` | 14 | |
| `rounded-4` | 16 | containers |
| `rounded-5` | 20 | |
| `rounded-6` | 24 | hero / large panels |
| `rounded-full` | — | radios, pills |

### Shadow
Keep depth subtle — borders and warm surfaces do most of the separation work.
- `shadow-arrow` = `0 4px 12px 0 rgb(0 0 0 / 0.16)` — for floating/overlay elements.
- `shadow-1px` = `inset 0 0 0 1px` green — crisp inset outline.
- **No heavy or dark drop shadows.**

### Layout
- **Container:** centered, `1rem` padding, max width **1314px** at `xl`/`2xl`.
- **Breakpoints:** `500px` · `sm` 640 · `md` 768 · `lg` 1024 · `xl` 1280 · `2xl` 1536.
- Mobile-first. Adapt the interface across sizes — don't hide critical functionality on mobile.
- For card grids, prefer self-adjusting `grid-template-columns: repeat(auto-fit, minmax(…, 1fr))`
  over manual breakpoints where it fits.

---

## 5. Buttons

Base class `.btn` + one variant + optional size. Defined in
[`button.css`](app/design/frontend/Valantic/base/web/tailwind/components/button.css).

```html
<button class="btn btn-primary">Voeg toe aan winkelwagen</button>
<button class="btn btn-secondary btn-size-sm">Meer informatie</button>
<a class="btn btn-tertiary" href="#">Bekijk details</a>
```

`.btn` base: flex/center, `gap-2`, `text-base`, `font-semibold`, `rounded-1`,
`transition-all`. Icon (`svg`) sits inline; label `<span>` is nudged for optical centering.

| Variant | Default | Hover / focus | Shape note |
|---------|---------|---------------|------------|
| `.btn-primary` | lime bg, white text, **4px bottom border** (light-green-shadow) | bg → light-green-shadow | the bottom border gives a subtle "physical" lift |
| `.btn-secondary` | transparent bg, green text, 1px green border | green bg, white text | outlined → filled on hover |
| `.btn-tertiary` | white bg/border, green text, **`p-0`** | text → lime | behaves like an inline link/ghost |

### Sizes
| Class | Padding | Text |
|-------|---------|------|
| `.btn-size-sm` | `px-4 py-1.5` (primary `pt-2 pb-1`) | 16px |
| (default) / `.btn-size-default` | `px-6 py-2.5` (primary `pt-3 pb-2`) | 16px |
| `.btn-size-lg` | `px-8 py-4.5` (primary `pt-5 pb-4`) | 24px (`text-6`) |
| `w-full` | full-width modifier | — |

### States
- **Hover:** real `:hover` or force with `.--hovered` (used by the style guide).
- **Focus:** removes default outline and applies the hover treatment — ensure a visible focus
  ring is preserved or added for keyboard users (see §9).
- **Disabled:** `:disabled` or `.--disabled` → `opacity-50 cursor-not-allowed`.

**Hierarchy:** one primary action per view. Use secondary for alternatives and tertiary for
low-emphasis/inline actions. Don't make everything primary.

---

## 6. Forms

Defined in [`forms.css`](app/design/frontend/Valantic/base/web/tailwind/components/forms.css)
(+ `forms/float_label.css`). `form` and `fieldset` are `flex flex-col gap-4` by default.

### Structure
```html
<div class="field field-reserved field-required">
  <label for="email">E-mail</label>
  <div class="control">
    <input class="form-input" id="email" name="email" type="email" required>
  </div>
</div>
```

### Inputs
`.form-input`, `.form-select`, `.form-textarea`: `w-full`, `text-4` (16px),
`px-3.5 py-3.5` (14px), 1px light-grey border, `rounded` (4px), `font-medium`.
- **Focus:** grey ring + grey focus border.
- **Disabled:** neutral-200 background.
- **`.form-select`** ships a chevron background icon with right padding.

### Field labels & required
`.field > label` is `text-3.5` (14px). Add `.field-required` (or `.required`) to render the
asterisk icon after the label.

### Validation states
- **Error:** `.field-error` → orange border + faint orange tint; for non-floating fields the
  `.control` gets the error icon, for floating fields the field does. `.messages` render in
  orange at 14px.
- **Success:** `.field-success` → lime border + check icon.
- **Warning:** `.warning` → grey text with an info icon.

### Choice controls
`.field-choice` (checkbox/radio) lays out as a row, `gap-3`, pointer cursor, 20px control.
- **Checkbox:** rounded, lime when `:checked`, light-grey when disabled.
- **Radio:** `rounded-full`, green radial fill when `:checked`.
- Focus shows the choice ring; error state borders go orange.

### Float-label variant
Add `.field-floating` (input *before* label in markup). See `forms/float_label.css`.

---

## 7. PageBuilder & content components

The theme extends Magento PageBuilder with Tuinmaximaal/Valantic blocks. Styles live in
[`components/valantic/pagebuilder/`](app/design/frontend/Valantic/base/web/tailwind/components/valantic/pagebuilder/)
and
[`theme/components/content-types/`](app/design/frontend/Valantic/base/web/tailwind/theme/components/content-types/):

- Image, Image + Text (with toggle variant), Image Gallery, Image Slider, Content Slider
- Main banner, Promo banner, Column group, Products, Blog posts
- USPs, Accordion, FAQ topics, SEO block, Showroom map, Image selling point

When building new content blocks, reuse these patterns and the semantic color/typography
classes above rather than styling from scratch.

---

## 8. Motion energy

Low and functional — motion confirms state, it never performs. Fits the trustworthy register.

- Animate **`transform` and `opacity` only**; never width/height/padding/margin.
- Use **ease-out** deceleration; **no bounce or elastic** easing (dated, undermines trust).
- `.btn` uses `transition-all`; keep durations short (~150–250ms).
- For expand/collapse (accordions, filters), prefer `grid-template-rows` transitions over
  animating `height`.
- Favor one well-orchestrated reveal over scattered micro-interactions.
- **Always honor `prefers-reduced-motion`** — drop non-essential motion to opacity or none.

---

## 9. Accessibility (WCAG 2.2 AA)

- **Contrast:** body green on white/sand and white on green/orange pass AA. **Check before
  shipping:** lime `#809700` and orange `#FF8000` text on light surfaces, and small text on
  sand/beige — these can fall below 4.5:1. Use green text on warm surfaces instead of grey.
- **Focus:** `.btn:focus` strips the default outline — always keep a visible focus indicator
  for keyboard users (focus ring or the hover treatment must be clearly perceivable).
- **Targets:** interactive controls ≥ 24×24px (choice controls are 20px — give them adequate
  surrounding padding / label hit area).
- **Motion:** honor `prefers-reduced-motion` (see §8).
- **Semantics:** use real `h1`–`h6` (they carry the heading styles), label every field,
  associate errors with `aria-describedby`.

---

## 10. Do / Don't

**Do**
- Use the semantic role classes and existing component classes; keep to the token scale.
- Keep it light, warm, and roomy; let sand/beige and space carry the design.
- Reserve orange and the highlight chip for true emphasis and primary actions.
- Lead with proof and structure at decision points — USP lists, reviews, guarantees, specs.
- Maintain one clear primary action per view.

**Don't**
- Introduce new fonts or off-brand colors, or hard-code hex values in markup.
- Go dark-mode or visually heavy; no heavy/dark drop shadows.
- Use aggressive sale-banner / loud coupon styling for promotions.
- Ship AI-slop tells: gradient text, decorative glassmorphism, colored `border-left`/`right`
  accent stripes (>1px) on cards/alerts, endless identical card grids, neon-on-dark accents.
- Make every button primary, or center everything by default.

---

_Generated via `/impeccable document` (Google Stitch DESIGN.md format). Update whenever the
theme tokens or component CSS change — the code in `base/web/tailwind/` remains the source of
truth._
