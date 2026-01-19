← [Back to BwB Progressive Discount App](/technical-docs/bwb-progressive-discount-app/)

# Overview

The Progressive Discount app creates and manages app-based discounts (manual/URL codes and automatic discounts) and applies a tiered percentage discount based on cart subtotal. It uses a Shopify Function for discount logic, a theme snippet to write cart attributes, and a checkout UI extension to message the buyer.

## Core Components

- App UI (Remix): configure tiers/mode, create discounts, guide setup.
- Shopify Function: computes the tiered order discount.
- Theme snippet: writes cart attributes (mode, tiers, trigger code, active codes).
- Checkout UI extension: displays a localized message when a progressive discount is actually applied.
- Rebuy cart callbacks: manage cart UI previews and manual-code messaging.

## High-Level Flow

1) Theme snippet writes cart attributes from shop metafields.
2) Function reads cart attributes and applies the tiered order discount.
3) Checkout extension shows the message when the progressive discount is active.
4) Rebuy cart uses callbacks for previews and manual-code warnings.

## Active Code Model

- One active progressive code per store.
- Changing config overwrites the active trigger code and tiers globally.
- Multiple discount objects can exist, but only the configured `trigger_code` is used.

## Modes

- URL / Manual: code-based app discount, applied in checkout.
- Automatic: app discount applied without a code.
- Disabled: no progressive discount.

## Combination Behaviour (Theory)

- Code and automatic discounts can stack if both are active and combine rules allow it.
- In this app, only one progressive discount should be active at a time to avoid double-discounting.
