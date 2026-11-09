# Comprehensive Accessibility & WCAG Conformance Audit

Act as an accessibility specialist, assistive technology expert, and WCAG conformance auditor conducting an exhaustive, production-grade accessibility audit of this repository and everything it deploys, configures, or depends on.

Review all markup, components, styles, interactive behavior, media, forms, documents, and generated content delivered to users.

Your objective is to identify **barriers for keyboard, screen reader, low-vision, motor, cognitive, and hearing-impaired users, and failures against WCAG 2.2 Level AA**.

Evaluate the system against mature, current industry standards (WCAG 2.2 AA, WAI-ARIA Authoring Practices, and Section 508 / EN 301 549 where relevant), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `ACCESSIBILITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Scope & Method

- **Surfaces:** List pages and components reviewed, and those reviewed only statically.
- **Static vs. Runtime:** Clearly separate findings confirmed in code from those requiring assistive technology testing.
- Map each finding to the specific WCAG success criterion.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Semantic Structure & Screen Readers

- **Semantic HTML:** Check landmarks, headings hierarchy, lists, tables, and native elements instead of clickable divs.
- **Accessible Names:** Check labels, alt text, icon buttons, and link purpose.
- **ARIA Usage:** Find incorrect, redundant, or conflicting roles and states; prefer native semantics.
- **Dynamic Content:** Check live regions, status messages, and route-change announcements.
- **Document Basics:** Check language, page titles, and zoom restrictions.

## 3. Keyboard & Focus

- **Operability:** Check that every function works without a mouse and without keyboard traps.
- **Focus Visibility:** Check visible, sufficiently contrasting focus indicators.
- **Focus Management:** Check modals, menus, drawers, route changes, and returned focus.
- **Tab Order:** Check logical order and misuse of positive tabindex.
- **Pointer Alternatives:** Check drag-only, hover-only, and small-target interactions.

## 4. Visual Design

- **Color Contrast:** Check text, UI component, and focus contrast ratios from actual values.
- **Color Dependence:** Find meaning conveyed only by color.
- **Reflow & Resize:** Check 200% zoom, 320px reflow, text spacing, and orientation.
- **Motion & Timing:** Check reduced-motion support, auto-playing content, and time limits.
- **Media:** Check captions, transcripts, and audio descriptions.

## 5. Forms, Errors & Remediation

- **Forms:** Check labels, instructions, required indicators, autocomplete tokens, and grouping.
- **Error Handling:** Check error identification, association with fields, and suggestions.
- **Authentication:** Check accessible authentication and CAPTCHA alternatives.
- **Remediation Plan:** Prioritize by user impact and WCAG level, and suggest automated tests (axe, lint rules) to prevent regression.

## 6. Evidence Standards & Calibration

- **Cite Evidence:** Every finding must reference concrete files, lines, configuration, queries, or observed behavior. Never fabricate evidence, metrics, or benchmarks.
- **Confirmed vs. Suspected:** Clearly label each finding as Confirmed (demonstrable from the code or configuration) or Risk (requires runtime, load, or environment verification).
- **Repository Limits:** Do not claim a control is absent merely because it is not visible in the repository. Report missing operational evidence separately.
- **No Name-Based Guessing:** Do not infer a defect solely from a file, variable, or column name.
- **Concrete Scenarios:** For each finding, describe the specific input, state, or sequence of events that produces the failure and who or what is harmed.
- **Acknowledge Strengths:** Record practices that are done well so they are preserved.

## 7. Required Report Structure

1. **Executive Summary:** Overall posture, the highest-impact risks, and a one-paragraph verdict.
2. **Inventory & Scope:** What was reviewed, what was not, and the assumptions made.
3. **Findings:** Each with ID, title, severity (Critical / High / Medium / Low / Informational), confidence, location, evidence, concrete failure scenario, impact, and recommended fix.
4. **Quick Wins:** Low-effort, high-value changes.
5. **Remediation Roadmap:** Prioritized phases with dependencies and rough effort (S/M/L).
6. **Verification Plan:** How each fix should be tested or measured once implemented.
7. **Open Questions:** Information needed from the team to close remaining uncertainty.
