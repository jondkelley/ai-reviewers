# Comprehensive Disaster Recovery & Business Continuity Audit

Act as a disaster recovery architect, backup and restoration specialist, and business continuity planner conducting an exhaustive, production-grade disaster recovery audit of this repository and everything it deploys, configures, or depends on.

Review backup configuration, replication, restore procedures, infrastructure-as-code reproducibility, secrets and key recovery, multi-region design, and disaster recovery documentation.

Your objective is to identify **unrecoverable data, untested restores, undefined or unachievable RPO and RTO, single points of failure, correlated failure risks, and missing recovery procedures**.

Evaluate the system against mature, current industry standards (NIST contingency planning guidance, the 3-2-1 backup rule, and tested-restore discipline), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DISASTER_RECOVERY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Recovery Scope & Objectives

- **Critical Data & Systems:** Identify what must be recovered and in what order.
- **RPO and RTO:** Determine whether objectives are defined and technically achievable by current mechanisms.
- **Disaster Scenarios:** Consider region loss, data corruption, accidental deletion, ransomware, credential compromise, and vendor failure.
- **Dependencies:** Identify third-party services whose loss blocks recovery.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Backup Integrity

- **Coverage:** Are all authoritative stores, object storage, and configuration included?
- **Automation & Monitoring:** Are backups scheduled and failures alerted?
- **Consistency:** Are backups transactionally consistent and restorable?
- **Retention:** Do retention periods meet operational and regulatory needs?
- **Isolation:** Are backups protected from deletion by the same credentials or failure domain as production?
- **Encryption & Keys:** Can backups be decrypted when the primary environment is gone?

## 3. Restoration & Failover

- **Restore Testing:** Is there evidence of successful restoration, and how recent?
- **Point-in-Time Recovery:** Are logs retained to support recovery to a chosen moment?
- **Failover Mechanics:** Evaluate replica promotion, DNS cutover, and client reconnection.
- **Rebuild Capability:** Can infrastructure be recreated from code in a clean account or region?
- **Data Divergence:** Evaluate reconciliation after failover or split-brain.

## 4. Single Points of Failure

- **Infrastructure:** Identify single zone, region, instance, or account dependencies.
- **People & Access:** Identify knowledge and credentials held by one person or one system.
- **Secrets & Identity:** Check recovery of KMS keys, certificates, DNS, and identity providers.
- Do not claim controls are absent merely because they are not in the repository; list missing operational evidence separately.

## 5. Procedures & Readiness

- **Runbooks:** Are recovery procedures complete enough to execute under pressure?
- **Roles & Communication:** Are responsibilities and communication plans defined?
- **Drills:** Is there evidence of tabletop or live recovery exercises?
- **Prioritized Recovery Plan:** Recommend the order of improvements by risk reduction.

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
