# Comprehensive Legacy Code, Dependency & Modernization Audit

Act as a software modernization architect, platform migration specialist, and dependency lifecycle analyst conducting an exhaustive, production-grade software modernization audit of this repository and everything it deploys, configures, or depends on.

Review language and runtime versions, frameworks, dependencies, build tooling, deprecated APIs, legacy patterns, configuration, and infrastructure definitions.

Your objective is to identify **obsolete or end-of-life technology, deprecated API usage, outdated patterns, upgrade blockers, accidental complexity, and opportunities to simplify using modern language, framework, and platform features**.

Evaluate the system against mature, current industry standards (vendor support lifecycles, semantic versioning, the strangler-fig migration pattern, and incremental upgrade practice), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `MODERNIZATION_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Technology & Lifecycle Inventory

- **Runtimes & Languages:** Identify versions and compare with vendor end-of-life dates.
- **Frameworks & Major Dependencies:** Identify versions behind current major releases and the size of the gap.
- **Build & Tooling:** Identify outdated bundlers, task runners, and CI images.
- **Infrastructure Versions:** Identify base images, database engines, and OS versions nearing end of support.
- Verify lifecycle claims against authoritative sources; do not guess dates.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Deprecated & Legacy Usage

- **Deprecated APIs:** Find calls that emit warnings or are scheduled for removal.
- **Legacy Patterns:** Find callback pyramids, class-based patterns replaced by modern idioms, manual polyfills, and hand-rolled utilities now provided by the platform.
- **Obsolete Dependencies:** Identify abandoned, unmaintained, or redundant packages.
- **Vendored & Forked Code:** Find copied libraries and local patches that block upgrades.
- **Compatibility Shims:** Find workarounds whose original reason no longer applies.

## 3. Upgrade Risk & Blockers

- **Breaking Changes:** Enumerate known breaking changes for each recommended upgrade.
- **Coupling to Old Versions:** Find code that depends on removed or changed behavior.
- **Test Safety Net:** Assess whether tests are sufficient to upgrade confidently.
- **Dependency Conflicts:** Identify peer-dependency and transitive constraints.
- **Ordering:** Determine the safe sequence of upgrades.

## 4. Simplification Opportunities

- **Platform Built-ins:** Identify custom code replaceable by standard library or framework features.
- **Dependency Reduction:** Identify packages that can be removed.
- **Dead Subsystems:** Identify features and code paths no longer used.
- **Configuration Sprawl:** Identify redundant or contradictory configuration.
- **Consolidation:** Identify duplicated tools doing the same job.

## 5. Modernization Roadmap

- **Incremental Plan:** Propose small, independently shippable steps with rollback points.
- **Effort & Value:** Rank each item by risk reduction and effort.
- **Do Not Rewrite:** Justify any recommendation larger than an upgrade or targeted refactor.
- **Success Criteria:** Define how completion of each step is verified.

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
