## Custom Cart and Discount Logic

### 1. `cart-items-custom.liquid` and `cart-discount-render.liquid`

**Purpose**

- These files handle UI updates in the cart drawer, simulating the application of discount codes to provide immediate visual feedback (e.g., price changes, discounts, error messages) to users before they proceed to checkout.

**Limitations**

- These files only update the front-end display and do not influence the actual discount applied at checkout. Their primary purpose is to improve the user experience by mimicking discount logic, though discounts are only truly applied at checkout when processed by the backend.

**Error Messages**

- Messages like "invalid code" or "discount applied" are generated based on validations in `discount_testing.js`, rather than by directly querying Shopify Admin.

### 2. Script Editor App

**Purpose**

- The Script Editor app enforces discounts during checkout by ensuring that the discounts displayed in the cart align with the final checkout total.

**How It Works**

- Scripts written in Ruby handle complex discount logic, such as 3-for-2 promos or bundle discounts, which are often not possible through Shopify's native discount system.
- The script can modify line item prices or properties (e.g., setting bundle tags) and apply the relevant discounts at checkout.

**Examples**

- **3-for-2 Promo**: Identifies eligible items, applies a discount to the least expensive item if there are three qualifying items.
- **Bundle Discounts**: Tags items with "Bundle" and adjusts line prices based on quantity thresholds, then applies the appropriate discounts.

**Script Migration**

- Shopify will deprecate the Script Editor app in 2024, requiring a shift to Shopify Functions or checkout extensions for replicating this discount logic.

### 3. Why VERSAND (example) Isn’t Working as Expected

**Shopify Discount Level**

- VERSAND is a free shipping discount created in Shopify Admin, designed to apply at checkout. It activates only when entered at checkout, not in the cart.

**Agency Workaround**

- Agency-created liquid templates (`cart-discount-render.liquid`, etc.) display discount codes in the cart drawer, giving users a visual confirmation of discounts pre-checkout. However, shipping discounts like VERSAND aren’t compatible with this workaround, as they activate exclusively at checkout.

**Current Behavior**

- When VERSAND is entered in the cart, the liquid templates show an error because `discount_testing.js` lacks a rule for this shipping discount. Since Shopify applies shipping discounts only at checkout, the cart drawer can't fully replicate this behavior without further customization.

### 4. `discount_testing.js` - Purpose and Limitations

**Purpose**

- `discount_testing.js` is a JSON-based file storing discount codes and validation rules (e.g., `discount_typ`, `minimum_price`, `value`, applicable products/collections). This file allows the cart UI to validate codes locally without constantly querying Shopify Admin, improving load times and user experience.

**Why It Exists**

- Shopify doesn’t provide direct access to discounts in the cart, so `discount_testing.js` allows for front-end validation against a local list of discounts.

**Limitations**

- Requires regular updates to reflect new or modified discounts from Shopify Admin, creating maintenance overhead.
- Only includes specific types of discounts (e.g., product or percentage discounts), and does not handle checkout-specific discounts like shipping discounts (e.g., VERSAND).

**Alternative**

- If discounts were solely applied via Shopify Admin, `discount_testing.js` could be removed. However, any custom discount logic unsupported by Shopify would require another solution.

### Additional Notes and Considerations

**Checkout Extensibility and Shopify Functions**

- With the Script Editor app deprecation, Shopify Functions will replace backend discount logic, requiring careful planning to accommodate complex discounts like the 3-for-2 promo.

**Discount Logic Duplication**

- Currently, discount logic is duplicated across front-end (`cart-discount-render.liquid`, `cart-items-custom.liquid`) and backend (Script Editor app), creating potential inconsistencies, especially with incompatible discount types (e.g., shipping).

**Future Improvements**

- Following the Script Editor deprecation, simplifying the front-end templates to align directly with Shopify Functions or creating a custom app for managing cart-level discount display/validation would provide a more streamlined approach.
