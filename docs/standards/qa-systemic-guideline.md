---
layout: default
title: QA Systemic Guideline
parent: Standards
---

# QA Systemic Guideline

Source: EXA-270 Exhaustive Prototype QA Protocol (Paperclip issue `35118d00-e8cc-48bb-8d75-582368284e92`, document `protocol`), hardened by board review on EXA-254. This guideline is the long-running version of those learnings. Where this page conflicts with the agent SDLC case EXA-C1, EXA-C1 wins for agent work.

## 1. Click every visible action, DOM-diff verified

- Enumerate roles first, then for each role x each nav tab: click the tab, wait for render settle, list all visible action buttons.
- Click every action button and record a DOM diff (forms/inputs/dialogs count plus body-text head/tail), not just a length delta. Toasts that replace toasts keep length constant, so assert on the toast text itself.
- Test each input-bearing flow twice: empty submit (must give feedback, never silent) and filled submit (must change state: toast plus rendered artifact).
- Verify state changes, not clicks: toggles flip confirmed state, cart math recomputes, status flips, message text appears in thread, filters narrow lists.
- Dead-button rule: a click producing zero DOM, text, or state change is a finding.
- Stub-toast-is-MAJOR rule: a click producing only a placeholder toast (for example a "(sample)" toast) where a form or real flow is expected is a MAJOR fidelity finding.

## 2. Design and aesthetic critique

- Token compliance: compare computed sidebar, active, and background colors against the brand kit hex values. Record exact matches and deviations.
- Contrast scan method: walk leaf text nodes, compute foreground/background ratio. Body text below 4.5:1 against its background in both themes is a finding with element plus colors. (The EXA-270 protocol's 2.0 figure was a coarse automated pre-scan on one prototype, not the bar.)
- Decorative-overlap (text-over-image) check: eyeball display type over background imagery at both themes. White text over light parts of a background image is a finding. Standard mitigations: scrim or gradient overlay, text shadow, or repositioning type off the busy area.
- Scaffolding check: design scaffolding sections (for example inspiration or scope-note blocks) must be hidden before any client send. Their presence on user-facing screens is a send-blocker.
- Accessibility minimums: record `h1` count, landmark presence (header, nav, main), named buttons, keyboard path for key flows (including Enter-to-send where a chat input exists), and font stacks ending in system fallbacks. No lorem, no emoji-as-icon overload, consistent title case.

## 3. Findings loop

- Severity scale: BLOCKING (data loss, breach, or outage in a realistic path) blocks merge or send; MAJOR (broken or stubbed flow, send-blocker) needs a fix or a recorded accepted risk; MINOR (copy, label, accessibility nits) rides along without blocking.
- Every finding carries file:line-equivalent evidence: role, tab, button, plus observed DOM, text, or command output. No evidence, no finding.
- File every MAJOR and above to the builder as a child issue with role, tab, button, and repro steps. MINORs ride along in the same issue.
- Track each finding and re-verify on the fixed build before the send verdict. The verdict records scope (exact range), BLOCKING items, non-blocking items, evidence, unreviewed areas, and handoff.
- Attachments minimum: desktop light and dark screenshots, phone light and dark screenshots, plus the machine-readable click log.

## 4. Standard pass shape

- Access precondition: if the target shows a login wall, stop. No verdict without rendering. Ask for a public link or sign-in.
- Viewports: full walk at desktop width, then re-walk key flows in the in-artifact phone simulator where applicable. Assert no horizontal overflow on every screen.
- Light and dark: read real theme state before and after each toggle click, never trust the toggle label. Flip both directions, including once after reload with a persisted theme.
- Robustness: install error and unhandled-rejection hooks at session start and report the log verbatim. Zero app errors required for PASS. Leave the app in its default state and close tabs opened during the pass.

## 5. Research note: lightweight practices worth knowing

- Risk-based testing: cover the highest-risk flows first (auth, payments, state-changing actions), then fill outward. Keeps small passes effective.
- Checklist over memory: a short written pass list (flows, viewports, themes, errors, design, findings) beats ad-hoc clicking and makes verdicts comparable across passes.
- Boundary and empty-state checks: empty submits, nonsense filter strings, and reload mid-flow catch silent failures cheaply.
- Screenshot discipline: same four screenshots every pass makes regressions visible without extra tooling.

## 6. Specialist agents for QA depth

- Keep the default QA pass with the QA Engineer. Add specialists only when the pass needs depth the generalist cannot give with evidence.
- Recommend: an accessibility specialist when the surface must meet a conformance target; a visual-design reviewer when brand or aesthetic maturity is in scope; a security reviewer for auth, payment, or data-exposure paths. Each specialist files findings through the same findings loop above, with the same evidence bar.
