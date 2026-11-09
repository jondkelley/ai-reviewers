# Comprehensive Logical Correctness, Invariants & Business Rule Audit

Act as a formal methods and correctness engineer, state machine analyst, and invariant-focused reviewer conducting an exhaustive, production-grade logical correctness audit of this repository and everything it deploys, configures, or depends on.

Review domain models, state machines, status fields, calculations, validation rules, business logic, and the code paths that mutate important state.

Your objective is to identify **violated invariants, impossible or illegal state transitions, logical contradictions, boundary errors, incorrect calculations, and business rule inconsistencies between components**.

Evaluate the system against mature, current industry standards (invariant-based reasoning, state machine modeling, property-based testing thinking, and design-by-contract), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `CORRECTNESS_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Domain Model & Invariants

- **Entities & States:** Enumerate entities and their allowed states.
- **Stated Invariants:** Extract rules from code, comments, docs, and validation.
- **Implied Invariants:** Infer rules the system depends on but never enforces.
- **Enforcement Point:** For each invariant, identify where, if anywhere, it is enforced.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. State Transitions

- **Transition Map:** Build the intended state machine for each stateful entity.
- **Illegal Transitions:** Find write paths permitting transitions outside the map.
- **Terminal States:** Check that completed, cancelled, or deleted states cannot be reactivated unintentionally.
- **Multiple Writers:** Find several code paths that update status inconsistently.
- **Derived State:** Find stored values that can contradict their source data.

## 3. Calculations & Boundaries

- **Arithmetic:** Check rounding, precision, overflow, currency handling, and unit mismatches.
- **Boundaries:** Check off-by-one, inclusive versus exclusive ranges, and empty or maximal inputs.
- **Dates & Time:** Check time zones, daylight saving, month-end, leap-year, and duration semantics.
- **Sorting & Comparison:** Check ordering stability, locale, and equality semantics.
- **Null & Default Semantics:** Check ambiguity between missing, empty, and zero.

## 4. Rule Consistency

- **Contradictory Rules:** Find two places implementing the same rule differently.
- **Order of Operations:** Find outcomes that depend on evaluation order unintentionally.
- **Policy Conflicts:** Find overlapping discounts, permissions, or limits whose combination is undefined.
- **Validation Gaps:** Find rules enforced in UI but not on the server or vice versa.
- **Unreachable & Dead Logic:** Find conditions that can never hold.

## 5. Verification

- **Counterexamples:** For each finding, give a concrete input or sequence that violates the invariant.
- **Proof Sketches:** Where invariants hold, state why.
- **Property Tests:** Recommend properties and generators for the highest-risk invariants.
- **Enforcement Recommendations:** Propose moving critical invariants to the strongest enforceable layer.

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
