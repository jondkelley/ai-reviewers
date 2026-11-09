# Comprehensive Product Completeness, Value & Workflow Audit

Act as a senior product manager, product strategist, and domain analyst conducting an exhaustive, production-grade product audit of this repository and everything it deploys, configures, or depends on.

Review implemented features, user flows, data model implications, configuration options, roadmap artifacts, issue trackers, and documentation that reveals intended product behavior.

Your objective is to identify **incomplete workflows, features of unclear value, unnecessary complexity, missing expected capabilities, inconsistent product rules, and gaps between apparent product intent and implemented behavior**.

Evaluate the system against mature, current industry standards (jobs-to-be-done, lifecycle completeness analysis, and outcome-oriented product management), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `PRODUCT_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Product Understanding

- **Purpose & Users:** Infer the product's purpose, user types, and core jobs from the code and docs; state assumptions explicitly.
- **Feature Inventory:** Catalogue implemented features and their maturity.
- **Intended vs. Actual:** Identify stubs, TODOs, hidden flags, and half-built features.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Workflow Completeness

- **Lifecycle Coverage:** For each major entity, check create, view, edit, archive, restore, delete, and history support.
- **Dead-End Flows:** Find paths that cannot be completed or reversed.
- **Edge Cases:** Check empty data, errors, permissions, and concurrent use from a user's viewpoint.
- **Roles & Handoffs:** Check that work can pass between roles without manual workarounds.

## 3. Value & Complexity

- **Feature Utility:** Identify features with no clear user need or evident usage.
- **Redundancy:** Find overlapping features and settings.
- **Configuration Burden:** Find options that push decisions onto users without benefit.
- **Complexity Cost:** Identify features whose maintenance cost outweighs likely value.
- Do not claim low usage without evidence; propose analytics to validate.

## 4. Missing Capabilities

- **Expected Features:** Identify capabilities users of this product category typically expect.
- **Operational Needs:** Check search, export, import, notifications, audit history, and reporting.
- **Integration Gaps:** Check connections users would reasonably require.
- **Onboarding & Help:** Check first-run experience and guidance.

## 5. Prioritization

- **Opportunity Matrix:** Rank findings by user value, risk, and effort.
- **Quick Wins vs. Strategic Bets:** Separate small completions from larger investments.
- **Success Metrics:** Propose measurable outcomes for each recommendation.
- **Questions for Stakeholders:** List decisions the team must make.

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
