← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Configuration

Configuration is stored as **shop metafields** under namespace `bwb_progressive`. This is a single, store-level configuration.

## Metafields

- `mode` (string): `off` | `manual` | `automatic`
- `trigger_code` (string): customer-facing code
- `step_1` (string): `amount/percent` (e.g. `30/10`)
- `step_2` (string)
- `step_3` (string)

## Behaviour

- Updating config overwrites the active progressive code and tiers globally.
- The function + checkout extension read the cart attributes written by the snippet.
- Only one trigger code is active per store.
- We can create lots of disocunts BUT our config setting is what guides the active trigger code, in terms of tiers and discounts

## Format rules

- Use whole numbers only (store currency, not cents).
- Example: `30/10`, `50/20`, `80/40`.

## Stored vs applied

- Config does not “attach” to a specific discount object. It drives whichever code is currently stored in `trigger_code`.
