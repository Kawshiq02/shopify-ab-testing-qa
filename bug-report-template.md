# Bug Report Template

## Title
_A short, specific summary. Bad: "Checkout broken". Good: "Discount code field accepts expired codes without error on Safari mobile"_

## Environment
- **Browser/Device:** e.g., Safari 17.4, iPhone 14
- **Environment:** Production / Staging / Local
- **URL:** Direct link to the page where the issue occurs
- **User state:** Logged in / Guest, New session / Returning
- **Experiment/Variant (if applicable):** Variant B, Experiment ID xyz

## Steps to Reproduce
1. Step one
2. Step two
3. Step three

## Expected Result
_What should happen_

## Actual Result
_What actually happens_

## Evidence
- Screenshot/screen recording
- Console log output (especially for React/JS issues)
- Network tab output if relevant (e.g., failed API call, missing tracking event)

## Severity / Priority

| Severity | Definition | Example |
|---|---|---|
| **Critical** | Blocks core revenue flow (checkout, payment) for all/most users | Payment fails for all cards on production |
| **High** | Blocks a key flow for a subset of users, or breaks tracking/data integrity | Discount code fails to apply on mobile Safari only |
| **Medium** | Functional but degraded experience; workaround exists | Cart drawer doesn't update quantity until page refresh |
| **Low** | Cosmetic or edge-case issue with minimal user impact | Minor spacing issue on a rarely-visited page |

| Priority | Definition |
|---|---|
| **P0** | Fix immediately — actively losing revenue or data |
| **P1** | Fix before next release |
| **P2** | Fix when convenient, scheduled into upcoming sprint |
| **P3** | Backlog, nice to fix eventually |

> Note: Severity describes *impact*. Priority describes *urgency to fix*. A cosmetic bug (Low severity) on the homepage during a major campaign launch could still be P1.

## Additional Notes
_Anything else relevant — related tickets, whether it's a regression, whether it's reproducible consistently or intermittently_

---
*Part of the [Shopify & A/B Testing QA Playbook](../README.md)*
