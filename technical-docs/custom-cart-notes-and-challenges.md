← [Back to Technical Documentation](/technical-docs/)

# Custom Cart Notes and Challenges

## 1. Current Setup

- Our cart shows discounts in real-time (like price changes or error messages) to improve the shopping experience, but the actual discounts are applied at checkout.
- We use custom templates for the cart visuals and a backend script to calculate the final discounts at checkout.

---

## 2. Current Issues

1. **Duplicate Work**

   - Discount rules are managed in two places: the cart visuals and the backend, making updates harder and increasing chances of errors.

2. **Checkout-Only Discounts**

   - Discounts like free shipping (`VERSAND`) only work at checkout, so they can’t always show properly in the cart.

3. **Shopify Changes**
   - Shopify might stop supporting URL-based discounts, which we rely on for passing discounts from the cart to checkout.

---

## 3. What We’re Doing Now

- Using a backend script to apply complex discounts, like "Buy 2, Get 1 Free," but Shopify is phasing out this tool by 2025.
- Testing a solution with Rebuy Smart Cart, which manages discounts directly in Shopify, making the cart simpler and easier to maintain.

---

## 4. Why Rebuy Smart Cart?

- Works seamlessly with Shopify’s built-in discounts, so we don’t need custom scripts or workarounds.
- Automatically shows accurate discounts in the cart without extra code or effort.

---

## 5. Next Steps

1. Test Rebuy Smart Cart in a non-live theme to see if it can handle all our discount scenarios (e.g., "Buy 2, Get 1 Free").
2. Start planning to migrate backend discount rules to Shopify Functions before 2025.
3. Simplify our cart visuals to rely more on Shopify’s built-in tools and less on custom code.

---

## TL;DR

- Our cart shows discounts but doesn’t apply them until checkout, which can confuse users.
- Rebuy Smart Cart looks like a simpler, easier solution to manage discounts moving forward.
- We need to test it thoroughly and plan for Shopify’s upcoming changes to keep things running smoothly.
