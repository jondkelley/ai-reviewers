# Comprehensive Code Quality & Maintainability Audit

Act as a staff software engineer, meticulous code quality reviewer, and maintainability specialist conducting an exhaustive, production-grade code quality audit of this repository and everything it deploys, configures, or depends on.

Review all source code, tests, scripts, and tooling configuration, including linters, formatters, type checkers, and CI quality gates.

Your objective is to identify **code smells, duplication, excessive complexity, dead code, anti-patterns, inconsistent conventions, unclear naming, weak error handling, and maintainability hazards**.

Evaluate the system against mature, current industry standards (Clean Code, Refactoring (Fowler), language-specific idioms and style guides), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `CODE_QUALITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Quality Baseline & Tooling

- **Language & Idioms:** Identify languages and frameworks and whether code follows their idiomatic practices.
- **Static Analysis:** Determine which linters, formatters, and type checkers exist and whether they are enforced.
- **Type Safety:** Find pervasive `any`, unchecked casts, ignored type errors, and missing annotations.
- **Consistency:** Identify competing conventions for naming, structure, and error handling.
- **Quality Gates:** Assess whether CI blocks regressions in lint, types, and tests.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Complexity & Structure

- **Function Size & Depth:** Find long functions, deep nesting, and high cyclomatic complexity.
- **Parameter Lists:** Find functions with excessive or boolean-flag parameters.
- **Large Files & Classes:** Locate files whose size indicates mixed responsibilities.
- **Control Flow:** Find convoluted branching, flag-driven behavior, and hidden side effects.
- **Hot Paths of Complexity:** Rank the worst offenders by risk, not only by metrics.

## 3. Duplication & Dead Code

- **Copy-Paste Logic:** Identify duplicated blocks that must be changed in lockstep.
- **Near Duplicates:** Find divergent copies that have already drifted apart.
- **Dead Code:** Locate unreachable branches, unused exports, orphan files, and stale feature flags.
- **Commented-Out Code:** Identify code retained in comments instead of version control.
- **Unused Dependencies:** Identify imports and packages that nothing uses.

## 4. Readability & Correctness Hazards

- **Naming:** Find misleading, abbreviated, or inconsistent names and overloaded terminology.
- **Magic Values:** Find unexplained literals, duplicated constants, and stringly typed logic.
- **Error Handling:** Find swallowed exceptions, empty catch blocks, generic errors, and lost stack context.
- **Null & Edge Handling:** Find unchecked nulls, off-by-one risks, and unhandled empty inputs.
- **Mutation & Side Effects:** Find functions that mutate arguments or global state unexpectedly.
- **Async Misuse:** Find unawaited promises, fire-and-forget calls, and callback/promise mixing.

## 5. Comments, Documentation & Tests as Quality Signals

- **Comment Quality:** Identify stale, misleading, or noise comments, and non-obvious logic lacking explanation.
- **Public Documentation:** Are public APIs and modules documented enough to use safely?
- **Test Readability:** Are tests clear, isolated, and meaningful or brittle and implementation-coupled?
- **Refactoring Priorities:** Recommend the smallest set of refactors yielding the largest maintainability gain.

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
