# Comprehensive CI/CD, Deployment Safety & Platform Engineering Audit

Act as a DevOps and platform engineering lead, release automation specialist, and build reliability engineer conducting an exhaustive, production-grade CI/CD and deployment audit of this repository and everything it deploys, configures, or depends on.

Review pipeline definitions, build scripts, containerization, deployment manifests, environment promotion, secrets handling in pipelines, rollback procedures, and developer workflow tooling.

Your objective is to identify **unsafe deployments, non-reproducible builds, missing rollback paths, environment drift, flaky or slow pipelines, weak quality gates, and unsafe pipeline permissions**.

Evaluate the system against mature, current industry standards (DORA metrics, twelve-factor app principles, trunk-based development, and progressive delivery practice), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DEVOPS_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Pipeline Inventory

- **Systems:** Identify CI/CD platforms, runners, and triggers.
- **Stages:** Map build, test, scan, package, deploy, and promote stages.
- **Environments & Promotion:** Document how a change reaches production and who or what approves it.
- **Manual Steps:** Identify undocumented or manual deployment actions.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Build Reproducibility & Quality Gates

- **Deterministic Builds:** Check lockfiles, pinned base images, and version floating.
- **Caching:** Evaluate cache correctness and poisoning risk.
- **Gate Enforcement:** Are tests, lint, type checks, and scans blocking, or advisory and bypassable?
- **Flaky & Slow Pipelines:** Identify retries masking failures and bottleneck stages.
- **Artifact Handling:** Is the artifact tested the same one deployed?

## 3. Deployment Safety

- **Strategy:** Evaluate rolling, blue/green, canary, and feature-flag usage.
- **Health Verification:** Are post-deploy checks automated, with automatic halt on failure?
- **Database Coordination:** Check migration ordering relative to code deploys.
- **Rollback:** Is rollback fast, tested, and safe given schema and data changes?
- **Concurrency Control:** Prevent overlapping deployments and out-of-order releases.
- **Configuration Changes:** Are config and secret changes versioned, reviewed, and reversible?

## 4. Pipeline Security & Permissions

- **Credentials:** Check long-lived secrets versus short-lived federation (OIDC).
- **Permission Scope:** Review token and runner privileges and third-party action pinning.
- **Untrusted Code:** Check handling of forks, pull requests, and script injection in workflow expressions.
- **Production Access:** Review who can deploy and how it is audited.

## 5. Environment Drift & Developer Experience

- **Parity:** Compare local, CI, and production environments.
- **Branching & Release Flow:** Evaluate branch strategy, protection rules, and review requirements.
- **Local Setup:** Assess onboarding time and documented reproducibility.
- **Metrics:** Assess lead time, deployment frequency, change failure rate, and recovery time evidence.
- **Toil:** Identify repetitive manual work suitable for automation.

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
