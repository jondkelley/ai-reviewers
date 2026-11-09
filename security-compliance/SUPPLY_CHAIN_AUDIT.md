# Comprehensive Software Supply Chain Security Audit

Act as a supply chain security engineer, dependency risk analyst, and build provenance reviewer conducting an exhaustive, production-grade software supply chain security audit of this repository and everything it deploys, configures, or depends on.

Review package manifests and lockfiles, transitive dependencies, build and release pipelines, container images, registries, vendored code, install scripts, signing, and artifact distribution.

Your objective is to identify **vulnerable or malicious dependencies, typosquatting and dependency confusion exposure, unpinned inputs, weak build provenance, missing SBOMs, unsigned artifacts, and compromised-pipeline risks**.

Evaluate the system against mature, current industry standards (SLSA, OpenSSF Scorecard, NIST SSDF, CycloneDX/SPDX SBOMs, and Sigstore practices), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `SUPPLY_CHAIN_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Dependency Inventory

- **Ecosystems:** Identify package managers, manifests, lockfiles, and registries.
- **Direct vs. Transitive:** Quantify the dependency tree and the riskiest branches.
- **Lockfile Integrity:** Check that lockfiles exist, are committed, and are honored in CI (frozen installs).
- **Vendored & Copied Code:** Identify embedded third-party source.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Vulnerabilities & Health

- **Known Vulnerabilities:** Use available audit tooling and advisories; cite CVE or advisory IDs and check reachability rather than reporting raw counts.
- **Abandonment:** Identify unmaintained, archived, or single-maintainer critical packages.
- **License Risk:** Flag incompatible or unclear licenses for counsel review.
- **Version Hygiene:** Check ranges, floating tags, and pre-release usage.
- Never invent advisories; state when a check could not be run.

## 3. Malicious Package & Confusion Risks

- **Typosquatting:** Look for lookalike package names.
- **Dependency Confusion:** Check private package names against public registry exposure and registry scoping.
- **Install-Time Code:** Review postinstall scripts and build hooks of dependencies.
- **Source Resolution:** Find git, URL, or tarball dependencies that bypass registry controls.
- **Suspicious Changes:** Note recent maintainer or ownership changes where evidence exists.

## 4. Build & Artifact Integrity

- **Pinned Inputs:** Check actions, base images, and tools pinned by digest or commit.
- **Provenance:** Check attestations, reproducible builds, and trusted builder use.
- **Signing & Verification:** Check artifact and image signing and verification at deploy.
- **Pipeline Hardening:** Check secrets exposure, token scope, and untrusted-code execution in CI.
- **Registry Security:** Check publish permissions, MFA, and tag immutability.

## 5. SBOM & Response

- **SBOM:** Check existence, completeness, and distribution.
- **Update Process:** Check automation (Dependabot, Renovate) and review practice.
- **Incident Readiness:** Check ability to identify exposure to a newly disclosed vulnerability quickly.
- **Prioritized Actions:** Rank by exploitability, exposure, and effort.

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
