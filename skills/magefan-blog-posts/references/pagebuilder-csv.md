# Magefan PageBuilder CSV Rules

Use these rules when generating `content` HTML for Magento PageBuilder inside Magefan blog CSV rows.

## Row Structure

Use one outer row per blog post content unless the existing import pattern clearly requires otherwise:

```html
<div data-content-type="row" data-appearance="contained" data-vice-versa-column="false" data-column-rounded-corners="false" data-column-media-rounded-corners="false" data-element="main">
  <div data-enable-parallax="0" data-parallax-speed="0.5" data-background-images="{}" data-background-type="image" data-video-loop="true" data-video-play-only-visible="true" data-video-lazy-load="true" data-video-fallback-src="" data-background-lazy-load="" data-element="inner" data-pb-style="LETTERID">
    ...
  </div>
</div>
```

Text-only PageBuilder blocks should be direct children of the row inner container:

```html
<div data-content-type="text" data-appearance="default" data-element="main">
  <div class="data-content-text-desktop" data-element="content">...</div>
</div>
```

Do not wrap ordinary text sections in columns. Use columns only for image sections, intentional multi-column layouts, or small constrained media beside related text.

## Column Group Contract

Every `Columns` section must use the full Magento attribute contract:

```html
<div class="pagebuilder-column-group"
  data-background-images="{}"
  data-content-type="column-group"
  data-appearance="default"
  data-grid-size="12"
  data-background-lazy-load="false"
  data-promo-banners-grid="false"
  data-row-auto-margins-padding="false"
  data-image-with-text-enabled="false"
  data-image-with-text-layout="horizontal"
  data-column-gap=""
  data-row-gap=""
  data-column-text-padding-one-side="false"
  data-column-text-padding-x="false"
  data-element="main"
  data-pb-style="LETTERID">
  <div class="pagebuilder-column-line" data-content-type="column-line" data-element="main" data-pb-style="LETTERID">
    ...
  </div>
</div>
```

For a one-column image section, use:

- `data-column-gap=""`
- `data-row-gap=""`
- one column with CSS `width:100%`

For a multi-column section, use:

- `data-column-gap="lg"`
- `data-row-gap="lg"`
- widths that sum to 100%, e.g. `75%` / `25%`, `50%` / `50%`, or `33.3333%` each

Every column group CSS rule must include:

```css
margin-top:1.5rem;
margin-bottom:1.5rem;
```

## Column Contract

Every column must use:

```html
<div class="pagebuilder-column"
  data-content-type="column"
  data-appearance="full-height"
  data-background-images="{}"
  data-background-lazy-load=""
  data-hover-enabled="false"
  data-hover-background-color=""
  data-hover-border-color=""
  data-element="main"
  data-pb-style="LETTERID">
  ...
</div>
```

The corresponding CSS must define the width:

```css
#html-body [data-pb-style=LETTERID] {
  justify-content:flex-start;
  display:flex;
  flex-direction:column;
  background-position:left top;
  background-size:cover;
  background-repeat:no-repeat;
  background-attachment:scroll;
  width:100%;
  align-self:stretch;
}
```

## Image Contract

Every PageBuilder image should use a figure with desktop and mobile images. Enable rounded corners through the PageBuilder image data attribute on every image variant:

```html
<figure data-content-type="image" data-appearance="full-width" data-element="main" data-pb-style="LETTERID">
  <img class="pagebuilder-mobile-hidden" src="{{media url=magefan_blog/example.jpg}}" alt="..." title="..." loading="auto" data-use-native-image-dimensions="true" width="auto" height="auto" data-desktop-image-width="auto" data-desktop-image-height="auto" data-rounded-corners="true" data-element="desktop_image" data-pb-style="LETTERID">
  <img class="pagebuilder-mobile-only" src="{{media url=magefan_blog/example.jpg}}" alt="..." title="..." loading="auto" data-use-native-image-dimensions="true" width="auto" height="auto" data-mobile-image-width="auto" data-mobile-image-height="auto" data-rounded-corners="true" data-element="mobile_image" data-pb-style="LETTERID">
</figure>
```

Image CSS:

```css
#html-body [data-pb-style=LETTERID]{border-style:none}
#html-body [data-pb-style=LETTERID]{max-width:100%;height:auto;border-radius:8px}
@media only screen and (max-width: 768px) { #html-body [data-pb-style=LETTERID]{border-style:none} }
```

Important: `border-radius` CSS alone does not mean the Magento PageBuilder rounded-corners toggle is enabled. Verify `data-rounded-corners="true"` on both desktop and mobile `<img>` elements.

## Media Paths

- Use `magefan_blog/file.ext` in CSV image fields.
- Use `{{media url=magefan_blog/file.ext}}` in content images.
- Avoid spaces in referenced media filenames. If the local source file contains spaces, create or use a safe lowercase hyphenated copy and reference that copy.
- Verify each referenced file exists in the source `magefan_blog` folder.

## `data-pb-style` IDs

- Generate uppercase alphanumeric IDs.
- Ensure every ID starts with a letter.
- Avoid substrings `NaN`, `NAN`, or other confusing tokens.
- Use the same ID consistently in HTML attributes and CSS selectors.
- Do not quote the CSS attribute selector; match Magento export style: `[data-pb-style=ABC1234]`.

## Verification Queries

When verifying with `lxml.html`, check:

- one row per post when intended
- direct text block count
- column-group / column-line / column counts
- image figure and `<img>` counts
- image order and file existence
- no spaces in referenced media paths
- every image variant has `data-rounded-corners="true"` when rounded images are expected
- rounded image CSS includes `border-radius`
- group CSS includes the 1.5rem margins
- no `NaN` / `NAN`
- no raw `®` outside `<sup>®</sup>`
