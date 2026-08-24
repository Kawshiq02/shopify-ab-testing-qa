# QA Notes for React-Based Storefronts

React-based storefronts (headless Shopify via Hydrogen, custom PDP/PLP builds, etc.) introduce bug categories that traditional server-rendered Shopify themes don't have. This is what I specifically watch for.

## 1. Hydration & Rendering Issues

- [ ] Server-rendered content matches client-rendered content on load (mismatch causes visible "flash" or console hydration warnings)
- [ ] Content that depends on client-only data (cart count, user session, A/B variant) doesn't flash the wrong state before hydrating
- [ ] Loading skeletons appear correctly instead of layout shift when async data is fetching

## 2. State Management Edge Cases

- [ ] Cart state stays in sync across multiple open tabs (or is intentionally isolated — confirm expected behavior)
- [ ] Navigating away mid-request (e.g., clicking checkout while a cart update is still in flight) doesn't cause stale state
- [ ] Browser back/forward navigation restores the correct component state (filters, scroll position, form inputs)
- [ ] Returning users see correctly restored state (wishlist, recently viewed) vs. new-session defaults

## 3. Client-Side Routing

- [ ] Direct URL access to deep routes (e.g., `/products/xyz?variant=123`) loads correctly, not just navigation via clicks
- [ ] Refreshing mid-flow (e.g., on a filtered collection page) preserves filters via URL params
- [ ] 404 and error boundaries render gracefully instead of a blank white screen
- [ ] Route transitions don't leave duplicate API calls firing (check network tab for redundant fetches)

## 4. Performance & Core Web Vitals

- [ ] Largest Contentful Paint (LCP) element is identified and isn't blocked by client-side JS execution
- [ ] Cumulative Layout Shift (CLS) is checked specifically around dynamically injected content (banners, A/B variants, ads)
- [ ] Interaction to Next Paint (INP) is reasonable on filter/sort actions on collection pages with large product counts

## 5. Cross-Browser & Device Considerations

- [ ] Test on Safari specifically — React apps often surface issues there first (date handling, flexbox/grid quirks, ITP-related storage issues)
- [ ] Test with JS-heavy browser extensions active (ad blockers) since they can interfere with client-side tracking/experiment scripts
- [ ] Low-end device testing (or CPU throttling in DevTools) to catch performance issues masked by dev machines

## 6. Working With Engineers on React Bugs

Tips that make bug reports on React apps far more actionable for engineers:
- Include the **component name** if visible in React DevTools, not just "the button"
- Note whether the issue reproduces on **hard refresh vs. soft navigation** — this alone often tells engineers if it's a hydration/state bug
- Capture the **console output**, not just a screenshot — React warnings often point directly at the root cause
- Note the **exact user flow** (e.g., "came from PLP via filter, not direct link") since React state bugs are often path-dependent

---
*Part of the [Shopify & A/B Testing QA Playbook](./README.md)*
