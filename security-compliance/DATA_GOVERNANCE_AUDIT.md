# Comprehensive Data Governance, Lineage & Retention Audit

Act as a data governance architect, data quality steward, and information lifecycle analyst conducting an exhaustive, production-grade data governance audit of this repository and everything it deploys, configures, or depends on.

Review data models across services, data ownership, lineage, retention and archival, deletion semantics, audit history, data quality controls, synchronization between systems, and analytics or reporting pipelines.

Your objective is to identify **unclear data ownership, inconsistent definitions, conflicting copies of data, undefined retention, inconsistent deletion semantics, missing history, poor lineage, and data quality failures**.

Evaluate the system against mature, current industry standards (DAMA-DMBOK principles, data lifecycle management, master data management practice, and data quality dimensions (accuracy, completeness, consistency, timeliness, uniqueness)), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DATA_GOVERNANCE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Data Asset Inventory

- **Datasets & Stores:** Catalogue tables, collections, files, caches, search indexes, and warehouses.
- **Ownership:** Determine which component or team owns each dataset and who may write to it.
- **Classification:** Classify by sensitivity and criticality.
- **Definitions:** Identify business terms and where definitions differ across the system.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Consistency & Lineage

- **Duplicate Copies:** Find the same fact stored in multiple places and how copies are synchronized.
- **Source of Truth:** Identify authoritative sources and derived data.
- **Sync Mechanisms:** Check how updates propagate and what happens on failure.
- **Conflicting Values:** Find cases where two systems can disagree without detection.
- **Lineage:** Check ability to trace derived or reported values to their origin.
- **Reporting Fidelity:** Check that analytics and exports match transactional data.

## 3. Retention, Archival & Deletion

- **Retention Rules:** Check defined periods and enforcement by code.
- **Deletion Semantics:** Compare hard delete, soft delete, anonymization, and archival across all stores.
- **Cascade Behavior:** Check what is removed or retained when parents are deleted.
- **Backups & Replicas:** Check how deletion interacts with copies.
- **Legal Holds:** Check ability to preserve data when required.

## 4. History & Auditability

- **Change History:** Check ability to see prior values and who changed them.
- **Temporal Correctness:** Check effective-dating, versioning, and point-in-time queries.
- **Immutable Records:** Check protection of records that must not change.
- **Reconstruction:** Test whether past states can be reconstructed for key entities.

## 5. Data Quality & Remediation

- **Validation:** Check input constraints and cleansing at entry points.
- **Quality Signals:** Check detection of duplicates, nulls, orphans, and anomalies.
- **Reconciliation Jobs:** Check periodic integrity checks.
- **Governance Process:** Check data change approval and schema ownership.
- **Prioritized Actions:** Rank by risk of incorrect decisions, compliance exposure, and cost to fix.

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
