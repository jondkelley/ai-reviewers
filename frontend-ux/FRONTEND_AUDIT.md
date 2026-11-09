# Comprehensive Frontend Architecture, State & Performance Audit

Act as a staff frontend engineer, UI architecture specialist, and web performance reviewer conducting an exhaustive, production-grade frontend engineering audit of this repository and everything it deploys, configures, or depends on.

Review all client-side code, components, routing, state management, data fetching, styling, build configuration, bundling, and browser-facing assets.

Your objective is to identify **component design flaws, state management defects, unnecessary re-renders, data-fetching anti-patterns, bundle bloat, memory leaks, fragile client logic, and frontend maintainability problems**.

Evaluate the system against mature, current industry standards (modern React/Vue/Svelte/Angular idioms as applicable, Core Web Vitals, and progressive enhancement), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `FRONTEND_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Frontend Inventory

- **Framework & Tooling:** Identify framework, version, bundler, language, and rendering mode (SPA, SSR, SSG, hybrid).
- **Routing & Entry Points:** Map routes, layouts, and code-split boundaries.
- **Component Library:** Identify shared, duplicated, and one-off components.
- **State Sources:** Catalogue local, global, server, URL, and form state.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Component Architecture

- **Responsibility:** Identify components mixing data fetching, business logic, and presentation.
- **Size & Nesting:** Find oversized components and deep prop drilling.
- **Reuse:** Find duplicated markup and logic that should be shared, and abstractions that obscure more than they help.
- **Props & Contracts:** Check typed props, default handling, and boolean-prop proliferation.
- **Composition:** Evaluate hooks, composables, and slots for correctness and reuse.

## 3. State & Data Fetching

- **State Placement:** Is state lifted too high, duplicated, or derived incorrectly instead of computed?
- **Server State:** Check caching, invalidation, deduplication, optimistic updates, and stale data.
- **Race Conditions:** Find fetches without cancellation that resolve out of order.
- **Loading & Error States:** Check every async view for loading, empty, error, and retry handling.
- **Forms:** Evaluate validation, dirty tracking, double submission, and data loss on navigation.

## 4. Rendering, Performance & Bundle

- **Re-renders:** Find unstable references, inline objects, missing keys, and expensive work in render.
- **Large Lists:** Check virtualization and pagination for big datasets.
- **Bundle Size:** Identify heavy dependencies, duplicate libraries, missing code splitting, and unused code.
- **Assets:** Check image sizing and formats, font loading, and lazy loading.
- **Memory & Lifecycle Leaks:** Find listeners, timers, subscriptions, and observers not cleaned up.
- **Core Web Vitals:** Assess likely LCP, INP, and CLS risks from the code.

## 5. Client Robustness & Maintainability

- **Browser Compatibility:** Identify unsupported APIs and missing fallbacks.
- **Client-Side Security Touchpoints:** Cross-reference unsafe HTML injection and token storage without duplicating the security audit.
- **Styling Architecture:** Evaluate CSS organization, specificity conflicts, and dead styles.
- **Testing & Types:** Assess component tests, type coverage, and error boundaries.
- **Developer Experience:** Evaluate build speed, linting, and conventions.

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
