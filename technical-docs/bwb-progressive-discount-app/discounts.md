← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Discounts

The app creates **app-based discounts** using Shopify Functions.

## Types

- **URL / Manual (code-based)**: customer enters or receives the code (including via URL). Title format: `CODE Progressive (URL/Manual)`.
- **Automatic**: applied without code. Title format: `CODE Progressive (Automatic)`.

## Activation

Only one progressive discount should be active at a time:

- URL / Manual active → Automatic inactive
- Automatic active → URL / Manual inactive

## Combining behaviour (theory)

- Code and automatic discounts can stack if both are active and combine rules allow it.
- The app currently allows combining classes; this can result in double-discounting.
- Operational rule: keep only one progressive discount active at a time.

## Function ID

The function ID is resolved dynamically and cached in the database. There is no hardcoded function ID.
