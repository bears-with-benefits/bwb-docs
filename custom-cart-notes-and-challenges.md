## Custom Cart Notes and Challenges in Plain English

### 1. Current Setup Overview

**Purpose**

- The current cart and discount setup provides users with visual feedback on discounts (e.g., applied discounts, error messages) directly in the cart drawer before they proceed to checkout. Note that all discounts created in Shopify's Admin are intended to be applied at checkout, not in the cart. Our method is a workaround to provide a better user experience.

**How It Works**

1. **Frontend (Cart UI):**

   - Custom templates (`cart-items-custom.liquid` and `cart-discount-render.liquid`) update the cart drawer's display to mimic Shopify discount logic.
   - Discounts are passed to the checkout via URL parameters.

2. **Backend (Script Editor):**

   - Discounts are enforced during checkout using custom Ruby scripts to handle complex discount scenarios (e.g., "3-for-2" promos).

**Limitations**

- The cart UI logic is purely cosmetic and does not influence the actual discounts applied at checkout, which are processed by the backend.
- Shopify’s evolving checkout restrictions may soon disallow URL-based discount applications. Checkout extensibility includes limiting the ability to manipulate checkout parameters via URLs (literally our entire approach). As a result, methods that involve appending discount codes directly to checkout URLs may not function as they once did (example source - https://community.shopify.com/c/shopify-discussions/discount-code-passed-as-a-query-parameter-to-checkout-but-it-s/m-p/2063987)
- Script Editor will be deprecated in August 2025, necessitating a migration to Shopify Functions or checkout extensions for discount logic.

---

### 2. Issues with the Current Setup

**Discount Logic Duplication**

- Discount rules are maintained across both:

  - **Frontend**: Liquid templates and JavaScript (`discount_testing.js`) for cart UI.
  - **Backend**: Script Editor app for final discount application during checkout.

- **Impact**: This duplication increases maintenance effort and risks inconsistencies.

**Checkout-Specific Discounts**

- Discounts in Shopify - like free shipping (`VERSAND`) - apply only at checkout.
- We can add visual feedback in the cart drawer, but the actual discount is only applied during checkout.

**Shopify Restrictions**

- Shopify’s new checkout setup may prevent URL-based discount passing, requiring an alternative solution for applying discounts from the cart.
- I found some issues with discount codes not adhering to the selected settings, e.g. "discount cannot be combined" is set in the Admin, but when we add it via a URL parameter, it still applies. This is the current issue with the workaround for the Versand code - it is always combinable, whihc we don't want.

---

### 3. Upcoming Challenges

**Script Editor Deprecation**

- Shopify will deprecate the Script Editor app in August 2025.
- This requires doing some research and migrating backend discount logic to **Shopify Functions** or **checkout extensions**.

**Incompatibility with Shopify’s New Checkout**

- Passing discounts via URLs from the cart may no longer work.
- Discounts will need to be applied directly at checkout or managed (?!) using Shopify Functions.

---

### 4. Examples of Current Discount Logic

**3-for-2 Promo**

- Backend (Script Editor):

  - Identifies three eligible items in the cart.
  - Discounts the least expensive item.
  - Checks for the tag `promo_product` to apply the discount

- Frontend (Cart UI):
  - Mimics this logic for display purposes but requires the backend script to actually enforce it during checkout.

**Shipping Discounts (`VERSAND`)**

- Backend:

  - Applies free shipping when the discount is entered at checkout.

- Frontend:

  - Displays an error in the cart drawer because shipping discounts are not supported by the custom cart logic. We can use the URL workaround method here, I have tried it and it functions - but this may not be supported in the future.

  ***

### 5. Key Considerations for Testing

**Testing Scope**

- Ensure cart and checkout totals match for all discount scenarios (e.g., "3-for-2" promos, shipping discounts).
- Validate different types of discounts (product-specific, percentage-based, shipping) across multiple countries (e.g., CH, IT).

**Expectations**

- Users should see consistent and accurate discount information from cart to checkout.
- Minimize user errors and confusion, particularly for discounts like `VERSAND`.

**Switchback Plan**

- Retain a backup of the current setup to quickly revert if issues arise during testing.

---

### 6. Proposed Next Steps

**Short-Term Goals**

1. Simplify the frontend logic:

   - Align cart templates directly with Shopify’s native discount system where possible.
   - Deprecate `discount_testing.js` to reduce maintenance overhead.

2. Plan for Script Editor migration:
   - Begin transitioning complex discount logic (e.g., "3-for-2" promos) to Shopify Functions.

**Long-Term Improvements**

1. Consolidate discount logic:

   - Use Shopify Functions to centralize discount rules and eliminate frontend-backend duplication.
   - Ensure future discount logic supports both cart and checkout seamlessly.

2. Future-proof against Shopify’s checkout restrictions:
   - Create a custom app or extension to manage cart-level discount display and validation without relying on URL parameters.

---

### 7. TLDR - Key Points to Consider

- Shopify discounts are intended for checkout, not the cart drawer.
- URL-based discount passing may soon be unsupported, requiring compliance with Shopify’s updated checkout rules.
- Testing must focus on both functionality (cart and checkout alignment) and user experience (error reduction, clarity).
