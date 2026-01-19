← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Rebuy Cart Behaviour

Rebuy SmartCart shows a discount input, but manual codes entered there are **preview-only**. Progressive codes are applied at checkout. URL and Auto discounts are checkout-level and thus applied in teh cart via Shopify / Rebuy (in theh case of single-item instances) or our callback code (if quantity > 1). For manual input codes, any potential workaround led to either weird behaviour or confusing UX. So, since manual code input is fewer than 20% of discount siutations, we simply added the below info.

## Manual Code UX

- If a buyer enters a progressive code in Rebuy, the app shows a localized message:
  - Example: “Progressive code detected — apply it at checkout to activate the discount.”
- This replaces the default “invalid code” error only when the entered code matches the progressive trigger code.

## Trigger Code Source

The theme snippet exposes the configured trigger code to JS:

```js
window.BwBProgressive = window.BwBProgressive || {};
window.BwBProgressive.triggerCode = "<trigger_code>";
```

## Callback Hook

- Rebuy callbacks listen for submit/error events.
- When an error message appears, the callback checks the entered code.
- If the entered code matches the trigger code, it overwrites the error message and applies a green info style.

## Store-specific variants

- Each store must ship a localized callbacks file (e.g., ES vs EN). This contains the relevant cart mesage for this particular UX workaround.
- Each store snippet must include the `triggerCode` global.
