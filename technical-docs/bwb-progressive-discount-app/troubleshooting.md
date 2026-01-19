← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Troubleshooting

## Discount message not showing in checkout

- Ensure the **Discount Watcher** block is enabled in Checkout Editor.
- Ensure a progressive discount is actually applied (manual code entered at checkout or automatic active).

## Manual code in Rebuy shows invalid error

- Confirm snippet exposes `window.BwBProgressive.triggerCode`.
- Confirm Rebuy callbacks file overrides the error message for matching code.

## Discounts not applying

- Verify the correct discount is active in Admin.
- Ensure only one progressive discount is active.
- Check cart attributes (`progressive_mode`, `step_1..3`, `progression_codes`).

## Function ID errors

- Ensure Prisma migration for `DiscountFunction` is applied.
- Ensure `SHOPIFY_API_KEY` matches the app key.

## Build errors on Vercel

- Ensure `prisma generate` runs at build/postinstall.
- Ensure `prisma migrate deploy` runs in prod.
