# Comprehensive Test Strategy, Coverage & Reliability Audit

Act as a principal QA automation architect, test strategist, and test reliability engineer conducting an exhaustive, production-grade testing audit of this repository and everything it deploys, configures, or depends on.

Review unit, integration, end-to-end, contract, performance, and security tests, fixtures, mocks, test data, test configuration, coverage tooling, and CI test execution.

Your objective is to identify **missing coverage on critical behavior, fragile or flaky tests, over-mocking, wrong test-pyramid balance, tests that cannot fail, slow suites, and gaps that allow regressions to reach production**.

Evaluate the system against mature, current industry standards (the testing pyramid/trophy, risk-based testing, mutation-testing thinking, and test isolation principles), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `TESTING_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Test Inventory & Strategy

- **Test Types:** Catalogue unit, integration, end-to-end, contract, and other tests and their proportions.
- **Tooling:** Identify frameworks, runners, and CI integration.
- **Documented Strategy:** Determine whether intent exists and matches reality.
- **Execution:** Determine what runs on every change versus nightly or manually.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Coverage of Risk

- **Critical Paths:** Map business-critical flows (auth, payments, permissions, data mutation) to their tests.
- **Coverage Metrics:** Distinguish line coverage from meaningful behavioral coverage.
- **Untested Code:** Identify risky modules with no tests.
- **Edge & Failure Cases:** Check boundaries, invalid input, timeouts, and error branches.
- **Regression Protection:** Check whether past bug fixes have regression tests.

## 3. Test Quality

- **Assertion Strength:** Find tests with no assertions, trivial assertions, or only snapshot checks.
- **Over-Mocking:** Find tests that mock the thing under test or so much that they verify nothing.
- **Implementation Coupling:** Find tests that break on refactoring without behavior change.
- **Readability:** Check naming, arrangement, and failure diagnosability.
- **Duplication:** Find copy-pasted tests and setup.

## 4. Reliability & Speed

- **Flakiness:** Find timing dependence, shared state, order dependence, randomness, and network reliance.
- **Isolation:** Check test data cleanup, parallel safety, and environment assumptions.
- **Determinism:** Check controlled time, randomness, and external services.
- **Suite Speed:** Identify slow tests and bottlenecks.
- **Retry Masking:** Find retries hiding genuine failures.

## 5. Gaps & Roadmap

- **Layer Gaps:** Identify missing integration, contract, E2E, and migration tests.
- **Non-Functional Testing:** Check performance, accessibility, and security test presence.
- **Prioritized Plan:** Rank new tests by risk reduction and cost, and name the specific scenarios to cover first.

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
