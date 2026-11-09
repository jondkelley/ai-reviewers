# Comprehensive Release Engineering & Backward Compatibility Audit

Act as a release engineering specialist, compatibility analyst, and change management reviewer conducting an exhaustive, production-grade release engineering audit of this repository and everything it deploys, configures, or depends on.

Review versioning scheme, changelogs, release workflows, tagging, packaging, feature flags, migration ordering, API and schema compatibility, rollback procedures, and release validation steps.

Your objective is to identify **unsafe release practices, breaking changes shipped silently, missing validation gates, unrealistic rollback, version inconsistencies, and incompatibilities between concurrently deployed versions**.

Evaluate the system against mature, current industry standards (Semantic Versioning, Keep a Changelog, progressive delivery, and expand-and-contract compatibility), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `RELEASE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Release Process Inventory

- **Versioning:** Identify the scheme and where versions are defined; check for inconsistency between manifests, tags, and artifacts.
- **Release Flow:** Document how a release is cut, built, validated, and published.
- **Automation vs. Manual:** Identify manual steps and who performs them.
- **Changelog & Notes:** Check completeness and accuracy.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Compatibility

- **Breaking Changes:** Identify API, schema, config, CLI, and event changes that break consumers.
- **Semver Honesty:** Check whether version bumps reflect actual change.
- **Rolling Deploy Safety:** Check that old and new versions can coexist (APIs, messages, database schema).
- **Client Compatibility:** Check mobile, SDK, and third-party consumers with slow upgrade cycles.
- **Deprecation:** Check notices, timelines, and removal discipline.

## 3. Validation Gates

- **Pre-Release Checks:** Check tests, smoke checks, migration dry-runs, and security scans required before release.
- **Staging Fidelity:** Check how closely staging resembles production.
- **Feature Flags:** Check flag hygiene, defaults, kill switches, and stale flags.
- **Progressive Rollout:** Check canary, percentage rollouts, and automated halting.
- **Post-Release Verification:** Check health checks and success criteria.

## 4. Rollback & Recovery

- **Rollback Feasibility:** Determine if rollback is possible after migrations, data changes, or sent messages.
- **Rollback Testing:** Check evidence of rehearsal.
- **Roll-Forward:** Check hotfix path speed and safety.
- **Artifact Retention:** Check availability of prior versions.
- **Communication:** Check release announcement and incident coordination.

## 5. Recommendations

- **Risk-Ranked Gaps:** Prioritize by blast radius of a bad release.
- **Release Checklist:** Propose a concrete checklist matching the project's actual process.
- **Metrics:** Recommend change failure rate and rollback time measures.

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
