← [Back to Technical Documentation](/technical-docs/)

## Custom Cart and Discount Logic

### 1. Frontend Logic `cart-items-custom.liquid` and `cart-discount-render.liquid`

**Purpose**

- Handle UI updates in the cart drawer to provide immediate feedback on discounts (e.g., price changes, discount notifications, or errors) before checkout.

**Limitations**

- Purely front-end and does not influence discounts applied at checkout. The backend determines final discounts, leading to potential discrepancies.

**Error Handling**

- Error messages like "invalid code" or "discount applied" are generated via `discount_testing.js`, without querying Shopify Admin.

---

### 2. Backend logic via Script Editor App

**Purpose**

- Enforces discount logic during checkout, ensuring cart drawer displays align with backend calculations.

**Examples**

- **3-for-2 Promo**: Applies a 100% discount to the cheapest item among qualifying groups of three.
- **Bundle Discounts**: Adjusts line item prices based on tagged bundles and quantity thresholds.

**Upcoming Change**

- The Script Editor app will be deprecated in August 2025, requiring migration to Shopify Functions or checkout extensions.

**Key Insight**

- As per the Shopify devs, passing a URL fragment for discounts is not a security risk or bot attack vector, addressing prior concerns.

## 3. Shipping Discounts: Case Study (`VERSAND`)

**Current Behavior**

- Shopify applies shipping discounts (like `VERSAND`) only at checkout. These are incompatible with cart drawer templates like `cart-discount-render.liquid`, leading to errors in the cart UI.

**Limitations**

- `discount_testing.js` cannot validate shipping discounts, as they activate solely during checkout.

**Future Direction**

- Rely on Shopify Admin to handle shipping discounts, eliminating redundant front-end logic.

---

## 4. Redundant Discount Validation (`discount_testing.js`)

**Current State**

- Stores discount codes and rules in JSON for local front-end validation.

**Problems**

- **Maintenance Overhead**: Periodic updates are needed to sync with Shopify Admin.
- **Complexity**: Requires 1,000+ lines of JavaScript for validation, error messages, and discount submission.

**Proposed Solution**

- Eliminate `discount_testing.js` entirely by migrating discount creation and validation to Shopify Admin, supported by Rebuy’s cart functionality.

---

## 5. Rebuy Smart Cart: Proposed Solution

**Why Rebuy?**

- Simplifies discount management by integrating with Shopify Admin, bypassing the need for custom discount logic in the theme.
- Automatically renders discount notifications and validates codes without custom scripts.
- Replaces the need for external server scripts uploading thousands of codes to the theme.

**Expected Benefits**

- **No Custom Validation**: Discounts and notifications are handled natively.
- **Streamlined Maintenance**: Direct integration with Shopify Admin eliminates the need for `discount_testing.js` and related scripts.
- **Reduced Complexity**: Removes reliance on agency-created Liquid templates and front-end validation scripts.

**Testing Plan**

- Trial Rebuy in a non-live theme to evaluate compatibility and functionality with the current setup.
- Verify Rebuy’s ability to handle complex discounts (e.g., 3-for-2 promo and bundle logic) during testing.

---

## Key Takeaways

- Rebuy Smart Cart offers a promising replacement for both front-end validation (`cart-discount-render.liquid`, `discount_testing.js`) and backend logic (Script Editor).
- Eliminating `discount_testing.js` simplifies maintenance and reduces theme complexity.
- Moving to Shopify Admin and Rebuy ensures a streamlined and maintainable discount solution moving forward.
