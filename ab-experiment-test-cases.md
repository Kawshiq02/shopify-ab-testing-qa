# Test Case Suite: A/B Experiment Validation

| ID | Title | Preconditions | Steps | Expected Result | Priority |
|---|---|---|---|---|---|
| AB-01 | Variant renders correctly on first load | Experiment is live, user not yet bucketed | 1. Clear cookies 2. Load target page | User sees either control or variant with no flicker between them | High |
| AB-02 | User stays in same variant across reloads | User already bucketed | 1. Load page, note variant 2. Refresh page 3. Repeat 3x | Same variant shown every time | High |
| AB-03 | Exposure event fires exactly once | Experiment live, analytics debug tool open | 1. Load target page 2. Check network/debug tool for exposure event | Exactly one exposure event fires per session, correct variant ID attached | High |
| AB-04 | Traffic split matches configuration | Experiment configured for 50/50 split | 1. Load page in 20+ incognito sessions 2. Tally variant shown each time | Roughly even split (allow for reasonable statistical variance) | Medium |
| AB-05 | Conversion event attributes to correct variant | User in Variant B completes target action (e.g., add to cart) | 1. Get bucketed into Variant B 2. Complete conversion action 3. Check analytics | Conversion event logged and attributed to Variant B | High |
| AB-06 | Variant doesn't break core functionality | Variant modifies a page element (e.g., button copy/placement) | 1. Load variant 2. Attempt core flow (e.g., add to cart, checkout) | Core flow completes with no errors introduced by the variant | High |
| AB-07 | No console errors introduced by experiment script | Experiment live | 1. Open browser console 2. Load page with variant active | No new JS errors compared to control page | Medium |
| AB-08 | Ad blocker / tracking prevention doesn't break bucketing | Safari with ITP enabled, or ad blocker active | 1. Load page with restrictive browser settings 2. Reload | User is still bucketed consistently, or gracefully defaults to control (per spec) | Medium |
| AB-09 | Experiment respects audience targeting rule | Experiment targeted to new visitors only | 1. Load as a returning visitor (existing cookie) 2. Load as a new visitor | Returning visitor sees control (unaffected); new visitor is eligible for bucketing | High |
| AB-10 | Variant is fully removed after experiment ends | Experiment marked as ended/archived | 1. Load target page after end date | Only control experience shows; no orphaned variant code or flicker | High |

---
*Part of the [Shopify & A/B Testing QA Playbook](../README.md)*
