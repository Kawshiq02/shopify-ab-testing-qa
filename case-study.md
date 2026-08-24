# Case Study: QA'ing an A/B Test on a High-Traffic Shopify Store

*A walkthrough of how I approach QA for experimentation on e-commerce sites, based on real-world practice. Details generalized/anonymized for a public example.*

## The Setup

A Shopify store running a React-based (headless) product listing page wanted to test a new experiment: moving product ratings from below the product title to above it, hypothesizing it would increase click-through to product pages. The test was configured in a third-party experimentation tool and set to run at a 50/50 split for two weeks.

## Pre-Launch QA Process

**1. Started with the experiment brief, not the code.**
Before touching the browser, I confirmed with the PM: What's the hypothesis? What's the primary success metric? Which pages and audience segments does this apply to? This matters because QA without knowing the *intent* of the test often misses the bugs that actually affect results (e.g., testing the wrong audience segment).

**2. Visual QA across variants.**
Loaded both variants across Chrome, Safari, and Firefox, desktop and mobile. Found that on Safari mobile, the reordered ratings element caused a layout shift that pushed the "Add to Cart" button below the fold on smaller product cards — a regression the design QA on desktop had missed entirely.

**3. Bucketing consistency check.**
Reloaded the page repeatedly in a fresh incognito session to confirm the same variant persisted. It did — but I also tested with Safari's Intelligent Tracking Prevention active, which revealed that returning visitors (who should've been excluded from the test per the targeting rule) were occasionally getting re-bucketed due to how the tool's cookie was being cleared by ITP. This was a targeting rule violation that would have quietly contaminated the results.

**4. Tracking validation.**
Using the analytics debug view, I confirmed the exposure event fired once per session and that the click-through conversion event correctly attributed to the variant the user actually saw — not the variant they were *originally* assigned before the ITP-related re-bucketing bug.

## What I Found

| Bug | Severity | Impact if shipped |
|---|---|---|
| Layout shift pushing CTA below fold (Safari mobile) | High | Would have suppressed conversions in the variant group specifically on Safari mobile, biasing results against the variant unfairly |
| ITP-related re-bucketing for returning visitors | High | Would have silently violated the targeting rule, mixing new and returning visitor data and invalidating the segment-level analysis |
| Minor: exposure event fired twice on slow 3G loads | Medium | Would have inflated exposure counts, skewing conversion rate calculations |

## Outcome

All three issues were fixed before the experiment launched. Because the re-bucketing bug was specific to Safari + ITP, it wouldn't have shown up in a "does the variant look right" pass — it only surfaced because I tested targeting logic under realistic privacy-restricted conditions, not just ideal browser conditions.

## Why This Matters for QA Strategy

The bugs that actually damage an A/B test aren't usually the ones that break the page visually — those get caught quickly. The dangerous ones are the ones that **quietly corrupt the data**: wrong bucketing, duplicate tracking events, or targeting rules that don't hold up under real browser privacy behavior. QA on experiments needs to validate the *measurement*, not just the *experience*.

---
*Part of the [Shopify & A/B Testing QA Playbook](./README.md)*
