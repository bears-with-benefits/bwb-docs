← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Ops and Deployment

## Hosting

- App hosted on Vercel.
- Repo is connected to Vercel; any push triggers an automatic redeploy.
- App URL: https://bwb-progressive-discount-app.vercel.app
- Vercel team dashboard: https://vercel.com/ians-projects-52a8fcf3
- Sessions stored in Neon Postgres via Prisma.

## Database

- Neon project dashboard: https://console.neon.tech/app/projects/rough-waterfall-49691746
- Connection string lives in `DATABASE_URL` (keep secret).

## Prisma

- `prisma generate` runs during `build` and `postinstall` in this repo (see `package.json`).
- `prisma migrate deploy` is **not** automatic unless you call `npm run setup` or wire it into your deploy pipeline.
- For Vercel, run `prisma migrate deploy` in production after deploy or add it to the build command.

## Function ID caching

- The app queries Admin API `appDiscountTypes` and caches the function ID in `DiscountFunction`.

## Logging

- Discount creation logs are stored in `DiscountLog` (DB).
- Serverless filesystem is read-only; do not write to files at runtime.

## Common env vars

- `SHOPIFY_API_KEY`
- `SHOPIFY_API_SECRET`
- `SHOPIFY_APP_URL`
- `SCOPES`
- `DATABASE_URL`

## Porting to another store

Use the same app instance for additional stores unless you explicitly want a separate app.

### Same app instance

- Install the app on the new store (Shopify Admin).
- Re-authorize if scopes changed.
- Run setup flow in the app:
  - Configure tiers + trigger code.
  - Create discounts.
  - Activate the correct discount in Admin.
  - Add the theme snippet and render line.
  - Enable the Discount Watcher block in Checkout Editor.
- No DB migration changes needed if you reuse the same Neon database.
