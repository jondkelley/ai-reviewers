# Comprehensive User Experience, Navigation & Task Flow Audit

Act as a principal UX designer, information architect, and interaction design reviewer conducting an exhaustive, production-grade user experience audit of this repository and everything it deploys, configures, or depends on.

Review every screen, route, navigation structure, form, modal, empty state, and user flow in the application.

Your objective is to identify **confusing information architecture, inconsistent interaction patterns, broken or lengthy task flows, dead ends, missing feedback, and obstacles to completing user goals**.

Evaluate the system against mature, current industry standards (Nielsen's usability heuristics, task-centered design, and established interaction patterns), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `UX_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Experience Inventory

- **User Types & Goals:** Identify roles and their primary tasks.
- **Screen & Route Map:** Catalogue all pages, states, and entry points.
- **Primary Flows:** Document key journeys step by step from the code and UI definitions.
- **Evidence Basis:** State clearly when conclusions come from code review rather than live observation.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Information Architecture & Navigation

- **Structure:** Is content grouped in a way that matches user mental models?
- **Navigation:** Check labeling, depth, wayfinding, breadcrumbs, and current-location indication.
- **Findability:** Check search, filtering, and shortcuts to frequent actions.
- **Dead Ends & Orphans:** Find pages with no onward path or no inbound link.
- **Role Awareness:** Check that users only see what is relevant to their role.

## 3. Interaction Consistency & Feedback

- **Pattern Consistency:** Check that the same action looks and behaves the same everywhere.
- **System Status:** Check loading, progress, success, and failure feedback.
- **Error Recovery:** Check that users can undo, correct, or retry.
- **Destructive Actions:** Check confirmation, reversibility, and clarity of consequences.
- **State Coverage:** Check empty, loading, error, partial, and offline states.

## 4. Task Completion

- **Flow Efficiency:** Count steps, clicks, and context switches for core tasks.
- **Form Design:** Check field order, defaults, validation timing, and progress preservation.
- **Decision Points:** Find choices that lack enough information to decide.
- **Mobile & Responsive:** Check task completion on small screens and touch input.
- **Interruptions:** Check behavior on refresh, back button, session expiry, and slow networks.

## 5. Prioritized Improvements

- **Severity:** Rank issues by effect on task success and frequency.
- **Recommendations:** Provide specific, implementable changes, not generic advice.
- **Validation:** Suggest usability tests or metrics to confirm improvements.

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
