← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Setup

This is the current merchant setup flow in the app UI.

## Step 1 — Add the theme snippet

- Create `snippets/progressive-discount.liquid` in the theme.
- Paste the latest snippet content.
- Add `{% render 'progressive-discount' %}` to `theme.liquid` (before `</body>`).

## Step 2 — Configure

In the app (Progressive Discounts page):

- Mode: URL / Manual, Automatic, or Disabled.
- Trigger code: the customer-facing code.
- Steps: `amount/percent` (store currency, whole numbers).

Manual codes cannot be applied in Rebuy cart. Use URL or Automatic in cart; manual codes must be entered in checkout. A localized message appears if a progressive code is entered in Rebuy.

## Step 3 — Create discounts

Use the app UI to create the discount objects for the trigger code.

## Step 4 — Enable the Discount Watcher block

- Shopify Admin → Settings → Checkout → Customize
- Add the **Discount Watcher** block
- Save

## Step 5 — Activate the right discount in Admin

- Shopify Admin → Discounts
- Activate only one progressive discount:
  - URL / Manual: enable “(URL/Manual)”, disable “(Automatic)”
  - Automatic: enable “(Automatic)”, disable “(URL/Manual)”

## One-code rule

Only one progressive code is active per store. Updating config switches the active code globally.
