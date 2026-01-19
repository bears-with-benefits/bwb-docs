← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Checkout Extension (Discount Watcher)

The checkout UI extension shows a localized message when a progressive discount is **actually applied**.

## Enablement

Merchants must add the **Discount Watcher** block in Checkout Editor:

- Shopify Admin → Settings → Checkout → Customize
- Add the block
- Save

## Localization

- Locales live in `extensions/discount-watcher/locales/*.json`
- Key used: `progressive.message`

## Display logic

- Uses `useDiscountCodes()` and `useDiscountAllocations()` to detect applied discounts.
- The banner is hidden if a progressive discount is not applied.

## Message content

Format is controlled by locale strings and uses placeholders for percentage and code.
