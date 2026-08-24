# Shopify QA Playbook

A testing guide covering the highest-risk areas of a Shopify storefront, based on where bugs actually tend to hide in production.

## 1. Theme & Storefront Testing

- [ ] Product pages render correctly across all variants (size/color combinations), including out-of-stock states
- [ ] Image galleries handle products with 1 image and products with 10+ images gracefully
- [ ] Price display is correct with and without active discounts, including compare-at pricing (strikethrough)
- [ ] Currency/locale switching (if multi-region) updates prices, not just the currency symbol
- [ ] Collection pages: filtering, sorting, and pagination all work together (not just in isolation)
- [ ] Search returns relevant results and handles typos/partial matches gracefully
- [ ] Theme customizer changes (from Shopify admin) reflect correctly on the live storefront without cache issues

## 2. Cart Testing

- [ ] Adding a product with variants (size/color) adds the *correct* variant, not a default
- [ ] Quantity updates recalculate price, tax, and shipping estimates correctly
- [ ] Cart persists correctly across sessions (logged in and guest)
- [ ] Removing the last item empties the cart cleanly (no broken empty-state UI)
- [ ] Cart drawer/mini-cart stays in sync with the full cart page (common source of bugs)
- [ ] Free shipping threshold messaging updates dynamically as items are added/removed

## 3. Checkout Testing

- [ ] Guest checkout and account checkout both complete successfully
- [ ] Discount codes apply correctly, including stacking rules (or correctly blocking stacking if not allowed)
- [ ] Discount codes correctly reject expired, invalid, or usage-limit-exceeded codes with a clear error
- [ ] Shipping options display correctly based on address/region entered
- [ ] Tax calculation is correct for the shipping destination (test at least 2–3 different regions)
- [ ] Payment failures (declined card, expired card) show a clear error and don't lose cart contents
- [ ] Order confirmation page and email both reflect the correct final total, items, and shipping details
- [ ] Abandoned checkout recovery emails trigger correctly (if enabled)

## 4. Discounts & Promotions

- [ ] Percentage vs. fixed-amount discounts calculate correctly at the line-item and order level
- [ ] Buy X Get Y promotions apply to the correct items, not arbitrary items in the cart
- [ ] Discounts respect product/collection exclusions defined in the rule
- [ ] Automatic discounts don't conflict unexpectedly with code-based discounts

## 5. App Integrations

- [ ] Reviews, loyalty, upsell, and subscription apps load without blocking page render
- [ ] Third-party app scripts don't introduce console errors or layout shift (CLS)
- [ ] Apps that inject UI (popups, widgets) don't overlap with theme elements or the cookie banner
- [ ] Removing/disabling an app doesn't leave orphaned scripts or broken references

## 6. Payment Gateway Testing

- [ ] Test all enabled payment methods (credit card, Shop Pay, PayPal, etc.) in sandbox/test mode
- [ ] Partial payment failures (e.g., 3D Secure authentication) are handled with a clear retry path
- [ ] Currency conversion at payment matches the displayed price

## 7. Inventory & Sync

- [ ] Out-of-stock products show correct messaging and disable "Add to Cart" appropriately
- [ ] Inventory decrements correctly after purchase and syncs across sales channels (if multi-channel)
- [ ] Backorder/pre-order logic (if used) is clearly communicated to the customer
- [ ] Low-stock warnings (if enabled) reflect actual inventory, not stale cache

---
*Part of the [Shopify & A/B Testing QA Playbook](./README.md)*
