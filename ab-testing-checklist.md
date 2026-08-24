# A/B Testing QA Checklist

A structured checklist for validating experiments before launch and monitoring them while live. Written for experiments run through tools like Optimizely, VWO, or Google Optimize/GA4 on Shopify or React-based storefronts.

## 1. Pre-Launch Validation

### Variant Rendering
- [ ] Each variant renders correctly across Chrome, Safari, Firefox, and Edge
- [ ] Mobile and desktop breakpoints both display the intended variant correctly
- [ ] No flicker/FOUC (Flash of Original Content) before the variant loads — especially critical on React sites where hydration can briefly show the control
- [ ] Variant doesn't break layout on slow network throttling (test on 3G simulation)
- [ ] Variant respects existing accessibility (contrast, tab order, screen reader labels) — not just visually correct

### Targeting & Bucketing
- [ ] Confirm audience targeting rules match the experiment brief (e.g., new vs. returning visitors, geo, device type)
- [ ] User is bucketed into the same variant consistently across page reloads and sessions (check cookies/local storage)
- [ ] Traffic allocation percentage matches configuration (e.g., 50/50 split isn't secretly 70/30)
- [ ] QA/internal traffic is properly excluded (or included) per test settings, so it doesn't skew results
- [ ] Test doesn't overlap/conflict with other running experiments on the same page or element

### Tracking & Analytics
- [ ] Experiment exposure event fires correctly for each variant (verify in GA4/Segment debug view or network tab)
- [ ] Event fires only once per session, not duplicated on re-renders
- [ ] Conversion goal events fire correctly for each step being measured (e.g., add-to-cart, checkout start, purchase)
- [ ] Revenue/order value data attributes correctly to the right variant in the analytics backend
- [ ] No tracking calls fire before consent is given, if the site uses a cookie consent banner

### Functional Regression
- [ ] Core site functionality (search, cart, checkout) still works normally within the variant
- [ ] No JS console errors introduced by the experiment script
- [ ] Page load time isn't significantly degraded by the experiment script (check Lighthouse/Core Web Vitals before/after)
- [ ] Variant doesn't break other integrations (reviews widgets, chat widgets, upsell apps)

## 2. During-Launch Monitoring

- [ ] Spot-check live traffic split matches configured allocation after 24–48 hours
- [ ] Monitor for anomalies in bounce rate or error rate specific to one variant
- [ ] Confirm sample ratio mismatch (SRM) isn't occurring — a sign of bucketing bugs
- [ ] Re-test on any new browser/OS version released during the experiment window
- [ ] Verify experiment still works correctly after any unrelated site deploys (experiments can silently break from CSS/DOM changes)

## 3. Edge Cases Worth Explicitly Testing

- [ ] User who bookmarks/shares a URL mid-experiment — does the variant persist correctly?
- [ ] User with ad blockers or tracking prevention (Safari ITP, Firefox ETP) — does bucketing still work, or does it default oddly?
- [ ] User switching devices mid-session (if the platform claims cross-device consistency)
- [ ] Direct traffic vs. traffic from paid ads — targeting rules sometimes differ
- [ ] Back button / browser cache — does the user see a flicker between variants?

## 4. Post-Test Wrap-Up

- [ ] Confirm the losing/control experience is fully removed or reverted (no orphaned code left live)
- [ ] Document any bugs found during the test for the next experiment cycle
- [ ] Verify final results reconcile with raw analytics data (not just the testing tool's dashboard)

---
*Part of the [Shopify & A/B Testing QA Playbook](./README.md)*
