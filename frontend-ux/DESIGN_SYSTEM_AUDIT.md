# Comprehensive Design System & Visual Consistency Audit

Act as a design systems architect, UI engineer, and visual design reviewer conducting an exhaustive, production-grade design system and visual consistency audit of this repository and everything it deploys, configures, or depends on.

Review stylesheets, theme configuration, design tokens, component library, typography, spacing, color usage, iconography, layout primitives, and component documentation.

Your objective is to identify **inconsistent components, hard-coded values bypassing tokens, typography and spacing drift, weak visual hierarchy, duplicated patterns, theming defects, and gaps in design system governance**.

Evaluate the system against mature, current industry standards (atomic design, design-token practice (W3C Design Tokens), and component API design principles), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DESIGN_SYSTEM_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. System Inventory

- **Sources:** Identify token definitions, theme files, component libraries, and any design files referenced.
- **Component Catalogue:** List shared components and their variants.
- **Adoption:** Measure how consistently shared components are used versus bespoke markup.
- **Documentation:** Check for a living style guide or Storybook.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Tokens & Foundations

- **Color:** Check palette scale, semantic naming, and hard-coded hex values.
- **Typography:** Check type scale, font stacks, line height, and weight usage.
- **Spacing & Sizing:** Check scale adherence versus arbitrary pixel values.
- **Elevation, Radius, Motion:** Check consistent shadows, corners, and animation timing.
- **Theming:** Check dark mode and theme-switching completeness.

## 3. Component Consistency

- **Variants:** Find near-duplicate buttons, inputs, cards, and modals.
- **States:** Check hover, focus, active, disabled, loading, and error states across components.
- **Component APIs:** Check naming, prop conventions, and composition patterns.
- **Layout Primitives:** Check grid, container, and breakpoint consistency.
- **Iconography & Imagery:** Check icon source, sizing, and alignment.

## 4. Hierarchy & Patterns

- **Visual Hierarchy:** Check emphasis, grouping, and density across screens.
- **Pattern Reuse:** Find the same problem solved multiple ways (tables, forms, alerts, pagination).
- **Responsive Behavior:** Check breakpoint consistency.
- **CSS Hygiene:** Find specificity wars, !important abuse, and dead styles.

## 5. Governance & Recommendations

- **Contribution Process:** Check how new components and tokens are proposed and versioned.
- **Migration Path:** Propose a staged path from bespoke styles to tokens and shared components.
- **Priorities:** Rank by visible inconsistency and effort.

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
