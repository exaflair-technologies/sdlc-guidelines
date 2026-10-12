---
layout: default
title: 5. QA System
parent: Delivery Workflow
nav_order: 5
---

# Step 5: QA System

QA is an independent, evidence-backed verification loop, not a blessing step.
Every finding becomes a tracked defect; every defect is re-verified.
No evidence, no finding. No defect record, no fix.

## The Loop

1. **Sweep** the candidate against this page's checklists. Record pass/fail per item with evidence.
2. **File** one child issue per failure (steps, expected, actual, environment, evidence). See [Bug Report Template](#bug-report-template).
3. **Triage** severity with the builder using the [severity scale](#severity). Blocking fails stop the release.
4. **Re-verify** each fix on the candidate build. Fixed-and-reverified closes the defect; anything else stays open.
5. **Record** the verdict (PASS / PASS-WITH-FINDINGS / BLOCK) on the QA issue with scope, evidence, and unreviewed areas.

## Thoroughness: Every Control Gets Clicked

Sampling the happy path is how dead buttons ship. The sweep rule, learned from EXA-254:

- Enumerate **every** button, link, tab, and form on **every** screen of **every** role. Click each one.
- For each control record the observable effect: navigation, dialog, form, toast, state change, or nothing.
- A control that shows a success message but performs no action is a **defect**, not a stub. Toasts must never claim an action that did not happen.
- Beware auto-advance/demo tours: if the candidate navigates without input, say so, and re-assert state before each probe so tour movement cannot masquerade as a click result.
- State explicitly what was **not** exercised. "Unreviewed" is a first-class section of every verdict.

## Design and Aesthetic Maturity Pass

Functionality passing is not enough for anything user-facing. Every QA run includes:

- **Contrast**: body text at least 4.5:1 against its background in both themes. Read every hero, banner, and overlay, not just body copy.
- **Overlap and clipping**: screenshot at a width matrix (e.g. 480 / 768 / 900 / 1024 / 1440) plus 125% zoom. Giant display type is the usual offender just above the responsive breakpoint.
- **Responsive bands**: check just above and below each layout breakpoint; that is where fixed-size elements overflow their cards.
- **Scaffolding leak**: design notes, lorem ipsum, sample toasts, and debug panels must not render in user-facing screens.
- **Copy**: spelling, singular/plural, and data consistency (names, roles, prices) across screens.
- **Accessibility floor**: landmarks, named controls, visible focus, keyboard reachability, no images without alt.

## Severity

Agree this before the run so the verdict cannot be negotiated after it:

- **BLOCKING**: data loss, breach, outage, or a dead core path in a realistic flow. Verdict: BLOCK.
- **MAJOR**: broken secondary flow, misleading success feedback, auto-behavior that hijacks the user. Verdict: PASS-WITH-FINDINGS, fix or record accepted risk.
- **MINOR**: copy, polish, consistency nits. Verdict: PASS-WITH-FINDINGS.

## Honesty Rules

- Could not reproduce is a result, not a failure. Report the exact matrix tried and hand the repro back to the builder.
- Never claim a test you did not run. Unknown stays unknown.
- Screenshots are evidence for a moment; state (hash, role, viewport, build) travels with every screenshot or it proves nothing.

## Bug Report Template

```text
Title: <Area>: <observable failure>
Severity: BLOCKING | MAJOR | MINOR (per scale above)

Steps: 1. ... 2. ... 3. ...
Expected: ...
Actual: ...
Environment: <build/version/URL, role, viewport, theme>
Evidence: <screenshot attachment, console output, or exact quote>
Refs: <QA issue id>
```

## Specialist Reviewers

Call one in when the risk warrants it; do not fake their expertise:

- **Visual/design critic** for brand compliance, typography, spacing, and AI-slop aesthetics on user-facing UI.
- **Accessibility specialist** for keyboard-only and screen-reader passes against WCAG 2.2 AA.
- **Security reviewer** for auth, payments, PII, and migration changes (independent pass, exploitability-scored).
- **Performance checker** for Core Web Vitals budgets (LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1) on key pages.
