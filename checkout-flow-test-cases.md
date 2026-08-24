# Test Case Suite: Shopify Checkout Flow

| ID | Title | Preconditions | Steps | Expected Result | Priority |
|---|---|---|---|---|---|
| CO-01 | Guest checkout completes successfully | Cart has 1+ in-stock item | 1. Go to checkout as guest 2. Enter shipping info 3. Select shipping method 4. Enter payment 5. Place order | Order confirmation page shows correct items, total, and order number | High |
| CO-02 | Logged-in checkout uses saved address | User has saved address on file | 1. Log in 2. Go to checkout 3. Confirm saved address is pre-filled | Saved address auto-populates correctly; user can still edit it | Medium |
| CO-03 | Valid discount code applies correctly | Cart total ≥ code's minimum spend | 1. Enter valid code at checkout 2. Apply | Discount reflected correctly in order summary; total recalculates | High |
| CO-04 | Expired discount code is rejected | Code with past expiry date | 1. Enter expired code 2. Apply | Clear error message shown; total unchanged | High |
| CO-05 | Out-of-stock item removed mid-checkout | Item goes out of stock while in cart | 1. Add item to cart 2. Simulate stock going to 0 3. Proceed to checkout | User is notified item is unavailable before payment is charged | High |
| CO-06 | Declined card shows clear error | Use test card configured to decline | 1. Enter declined test card 2. Submit payment | Clear decline error shown; cart contents preserved; user can retry | High |
| CO-07 | Tax calculates correctly by region | Shipping address in a taxed region | 1. Enter address 2. Review order summary | Tax amount matches expected rate for that region | Medium |
| CO-08 | Shipping options match address | Address in a region with multiple shipping tiers | 1. Enter address 2. View shipping options | Only valid options for that region appear, correctly priced | Medium |
| CO-09 | Order confirmation email matches order summary | Order successfully placed | 1. Complete order 2. Check confirmation email | Email totals, items, and shipping match what was shown at checkout | High |
| CO-10 | Back button after order placement doesn't duplicate order | Order successfully placed | 1. Complete order 2. Click browser back button 3. Click "Place Order" again if visible | No duplicate order is created; user is redirected appropriately | High |
| CO-11 | Abandoned checkout triggers recovery email | Recovery emails enabled in admin | 1. Start checkout 2. Enter email 3. Abandon before payment 4. Wait for trigger window | Recovery email is sent to the entered email with correct cart contents | Low |
| CO-12 | Multiple currency checkout shows correct totals | Store has multi-currency enabled | 1. Switch currency 2. Proceed to checkout | All totals (subtotal, tax, shipping) reflect the selected currency correctly | Medium |

---
*Part of the [Shopify & A/B Testing QA Playbook](../README.md)*
