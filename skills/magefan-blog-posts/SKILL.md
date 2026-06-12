---
name: magefan-blog-posts
description: Create or update Magento Magefan blog post CSV imports from DOCX/blog source content and media folders. Use when adding localized Magefan blog rows, translating blog posts, generating PageBuilder-safe content HTML, assigning store views/post IDs/identifiers/images, preserving DOCX formatting, or verifying Magento blog_posts.csv import data.
---

# Magefan Blog Posts

## Core Workflow

Use this skill for Magefan blog imports in `blog/posts/blog_posts.csv`.

1. Read the source DOCX/content file, local `magefan_blog` media folder, and target CSV schema before editing.
2. Use `$tuinmaximaal-translator` for Tuinmaximaal/Gumax terminology when translating.
3. Use `$seo` for image alt/title text and metadata improvements, without changing article meaning.
4. Create one CSV row per language/store view. Preserve every existing CSV column and fill only the relevant fields.
5. Build PageBuilder HTML using the rules in `references/pagebuilder-csv.md`.
6. Add or update the rows in the master import file `blog/posts/blog_posts.csv` unless the user explicitly asks for a standalone CSV only.
7. If a standalone per-post CSV is also created, keep its rows aligned with the corresponding rows in the master import file.
8. Verify the import data structurally after writing the CSV.
9. Remove temporary scripts and do not stage or commit unless the user explicitly approves it.

## Store Views And IDs

Use the existing import rows as source of truth. Current project defaults:

- Dutch: `store_ids` = `2,3`
- German: `store_ids` = `5`
- French: `store_ids` = `6,7`
- English: `store_ids` = `9`

When the user gives new post IDs, assign one row per language in the requested order. Keep identifiers localized and lowercase with hyphens.

## Import Visibility

- Treat the master file `blog/posts/blog_posts.csv` as the file Magento import jobs are most likely to consume.
- Do not leave finished posts only in a blog-specific CSV unless the user explicitly says that file is the import target.
- Compare new rows with known visible rows for `is_active`, `include_in_recent`, `publish_time`, `categories`, `store_ids`, `author_id`, and `enable_comments`.
- Use `is_active=1`, `include_in_recent=1`, and a non-future `publish_time` aligned with nearby working rows unless the user asks to schedule the post.
- Set `categories` to the same blog category as comparable visible posts when the user does not specify another category.
- After writing, verify every new post ID appears in the actual import CSV and not only in a temporary or per-post export.

## Content Handling

- Treat DOCX headings like `Tekst NL`, `Tekst DE`, `Tekst FR`, `Tekst ENG` as language section boundaries.
- Preserve article meaning. Do not invent content beyond light SEO metadata and image alt/title text.
- Preserve DOCX formatting that affects reading: convert bold inline runs or bold lead-in phrases to `<strong>...</strong>` unless the paragraph is already represented as a heading.
- Use `<sup>®</sup>` for registered symbols inside content HTML.
- Keep text blocks directly inside the PageBuilder row unless the design truly needs columns.
- Use `<ul>` / `<li>` for list-like DOCX content and for clear list runs introduced by wording like "Door deze behandeling:" or "Daarnaast biedt het materiaal:".
- Keep links, product names, brand names, and Magento media macros intact.

## Images

- Read the local `magefan_blog` folder for available images and map each image to its DOCX position or user-specified order.
- Avoid spaces and unsafe characters in Magento media filenames. If a source filename contains spaces, create or use a safe lowercase hyphenated copy and reference that path in CSV fields and `{{media ...}}` macros.
- Use `featured_img` with a `magefan_blog/...` path, not a `{{media ...}}` macro.
- Use content images as `{{media url=magefan_blog/file.ext}}`.
- Add localized `alt` and `title` to every desktop and mobile `<img>`.
- Use desktop and mobile image variants inside each PageBuilder image figure.
- Enable the PageBuilder rounded-corners toggle on every image variant with `data-rounded-corners="true"`; do not rely on `border-radius` CSS alone.
- Add matching rounded-corner CSS such as `border-radius:8px` when rounded images are expected.
- If an image should be constrained, such as a small certification/logo image, use an intentional column layout and explicit max-width while keeping the Magento column contract valid.
- If the user specifies exact image order, verify the content paths match that order exactly.
- Remember: the CSV can reference images, but Magento must also have those files in its media storage on the target environment.

## Verification Checklist

After editing, verify at minimum:

- Expected post IDs, store views, identifiers, titles, metadata, and featured images are present.
- CSV row count and column names are preserved.
- New rows are present in `blog/posts/blog_posts.csv` or the exact import CSV requested by the user.
- If both master and standalone CSVs exist, matching post IDs have identical row data in both files.
- Visibility fields match working posts: `is_active=1`, `include_in_recent=1`, non-future `publish_time`, populated `categories`, and correct `store_ids`.
- Each edited content field parses as HTML.
- PageBuilder has no corrupt column markers such as `NaN` or `NAN`.
- `data-pb-style` tokens start with letters.
- Text-only sections are direct row children, not unnecessary columns.
- Column groups use the exact Magento attribute contract from `references/pagebuilder-csv.md`.
- Every column group has `margin-top:1.5rem` and `margin-bottom:1.5rem`.
- Image paths point to existing files under the source `magefan_blog` folder and do not contain spaces.
- Every `<img>` has non-empty `alt` and `title`.
- Every desktop and mobile `<img>` has `data-rounded-corners="true"` when rounded images are expected.
- Rounded images include both the PageBuilder toggle and CSS, not just one of them.
- DOCX bold runs that remain paragraph text are represented with `<strong>`.
- Content uses `<sup>®</sup>` and contains no raw `®` outside that markup.
- No Unicode replacement character `\ufffd` exists in edited rows.

Use small temporary Python scripts when needed for DOCX parsing, CSV writing, and HTML verification. Delete those scripts before finalizing.
