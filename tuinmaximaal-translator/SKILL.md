---
name: tuinmaximaal-translator
description: Brand-sensitive translation for Tuinmaximaal product, ecommerce, marketing, and customer-service copy. Use when translating or reviewing text that contains Tuinmaximaal or Gumax® terminology and must follow the approved Dutch-based glossary for English (UK), French, Dutch, and German workflows. Preserve official product names, formal customer-facing tone, and language-specific formatting rules.
---

# Tuinmaximaal Translator

## Workflow

1. Detect the source and target language from the user request.
2. Treat Dutch as the canonical glossary source for official Tuinmaximaal terminology and load only the matching reference file:
   - Dutch <-> English (UK): `references/EN.md`
   - Dutch <-> French: `references/FR.md`
   - Dutch <-> German: `references/DE.md`
3. Use the Dutch term on the left side of the selected reference as the source of truth for official Tuinmaximaal and Gumax® product terminology.
4. Use glossary terms before free translation. Keep approved product names intact and adjust only the surrounding grammar.
5. Use the glossary for brand-specific terminology and approved product names. Translate generic, non-glossary wording naturally in the target language.
6. Keep the glossary focused on brand-specific terminology. Do not add general-purpose dictionary terms, generic adjectives, broad UI labels, or other low-risk generic wording.
7. Preserve official formatting such as `Gumax®`, product capitalization when it remains grammatical, the formal customer-facing tone, and the punctuation rules from the selected reference.

## Language Routing

- Handle English (UK) <-> French, English (UK) <-> German, and French <-> German only when both non-Dutch terms can be mapped safely through the approved Dutch glossary rows.
- Decline direct pairs that have no safe Dutch-based path in the references.

## Output Rules

- Return the translation only, unless you need to flag a missing or ambiguous glossary term.
- When you flag a missing or ambiguous term, keep the note short and actionable.
- Keep currencies and other language-specific wording aligned with the selected reference.
- Before returning the result, quickly check that every obvious Tuinmaximaal or Gumax® product term matches the glossary.
