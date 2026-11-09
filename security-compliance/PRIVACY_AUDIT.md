# Comprehensive Privacy, PII Exposure & Data Minimization Audit

Act as a privacy engineer, data protection analyst, and privacy-by-design reviewer conducting an exhaustive, production-grade privacy engineering audit of this repository and everything it deploys, configures, or depends on.

Review data collection, storage, processing, logging, analytics, third-party sharing, retention, deletion, consent mechanisms, exports, and data subject request handling.

Your objective is to identify **PII exposure, over-collection, indefinite retention, missing consent handling, incomplete deletion, uncontrolled third-party data flows, and weaknesses in privacy-by-design**.

Evaluate the system against mature, current industry standards (GDPR and CCPA/CPRA principles, ISO/IEC 27701, NIST Privacy Framework, and privacy-by-design), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `PRIVACY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Personal Data Inventory

- **Data Elements:** Catalogue personal and sensitive data collected (identifiers, contact, financial, health, location, behavioral).
- **Data Flow Map:** Trace each element from collection through storage, processing, sharing, and deletion.
- **Purpose Mapping:** Identify the stated or evident purpose of each element.
- Legal conclusions are outside scope; flag issues for counsel review rather than asserting compliance or violation.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Minimization & Exposure

- **Over-Collection:** Find fields collected without a clear need.
- **Over-Exposure:** Find APIs, exports, logs, and error messages returning more personal data than necessary.
- **Logging & Telemetry:** Find PII in logs, analytics, error trackers, and URLs.
- **Non-Production Data:** Find production data in dev, test, or fixtures.
- **Pseudonymization & Encryption:** Check protection of sensitive fields at rest and in transit.
- **Access Scope:** Check which roles and staff can view personal data.

## 3. Retention, Deletion & Data Subject Rights

- **Retention Rules:** Check defined periods and automated enforcement.
- **Deletion Completeness:** Trace deletion across databases, caches, search indexes, backups, files, logs, and third parties.
- **Soft Delete Reality:** Find "deleted" data that persists.
- **Access & Export:** Check ability to retrieve a person's data.
- **Correction & Restriction:** Check update propagation and processing restriction.

## 4. Consent & Third Parties

- **Consent Handling:** Check capture, storage, withdrawal, and enforcement before processing.
- **Cookies & Trackers:** Check loading of non-essential trackers before consent.
- **Third-Party Processors:** Identify SDKs, analytics, payment, email, and AI services receiving personal data.
- **Cross-Border Transfers:** Identify regions where data is processed or stored.
- **Children & Special Categories:** Check handling of sensitive classes of data.

## 5. Governance & Remediation

- **Records & Audit:** Check evidence of processing records and access logging.
- **Incident Readiness:** Check breach detection and notification capability.
- **Prioritized Fixes:** Rank by data sensitivity, volume, and exposure.

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
