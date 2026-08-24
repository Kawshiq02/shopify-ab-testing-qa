# Shopify & A/B Testing QA Playbook

A practical, field-tested QA reference for validating A/B experiments and Shopify/React e-commerce sites — built from real-world senior QA practice.

This isn't a generic QA template. It's the actual checklists, test cases, and processes I use to catch the bugs that generic testing misses: broken variant assignment, silent tracking failures, checkout edge cases, and React hydration issues that only show up in production.

## 📂 What's in this repo

| File | Purpose |
|---|---|
| [`ab-testing-checklist.md`](./ab-testing-checklist.md) | Full QA checklist for validating A/B tests before and during launch |
| [`shopify-qa-playbook.md`](./shopify-qa-playbook.md) | Testing guide covering theme, cart, checkout, discounts, and app integrations |
| [`react-site-qa-notes.md`](./react-site-qa-notes.md) | QA considerations specific to React-based storefronts |
| [`test-cases/`](./test-cases) | Structured test case suites for checkout, A/B experiments, and cart flows |
| [`templates/bug-report-template.md`](./templates/bug-report-template.md) | Bug report format with severity/priority matrix |
| [`case-study.md`](./case-study.md) | Walkthrough of how I QA'd a real A/B test on a high-traffic Shopify store |

## 🎯 Why this exists

Most public QA portfolios are automation-heavy and generic. In e-commerce and experimentation, the highest-value bugs are usually **not** "the button doesn't click" — they're things like:

- A variant that renders correctly but never fires its tracking event
- A discount code that works in Chrome but silently fails in Safari's ITP-restricted state
- A React component that re-renders correctly for new sessions but shows stale state for returning users
- An experiment bucketing users inconsistently across page reloads

This playbook is built around catching *those* bugs.

## 👤 About

Built by **Ariful Hasan Kawshiq**, Senior QA Engineer at Echologyx, focused on A/B testing and Shopify/React e-commerce QA.
