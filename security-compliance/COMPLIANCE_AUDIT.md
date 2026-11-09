# Comprehensive Compliance, Governance & Audit Trail Audit

Act as a compliance and governance specialist, internal audit analyst, and control-mapping reviewer conducting an exhaustive, production-grade compliance and governance audit of this repository and everything it deploys, configures, or depends on.

Review policy and control implementation in code and configuration, audit logging, access controls, data handling, change management, retention, and documentation relevant to applicable regulations.

Your objective is to identify **regulatory exposure, missing or weak audit trails, unenforced policies, inadequate evidence for controls, data-handling violations, and gaps between documented policy and implemented behavior**.

Evaluate the system against mature, current industry standards (SOC 2 trust services criteria, ISO 27001 Annex A, PCI DSS, HIPAA, GDPR, and sector rules identified as applicable), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `COMPLIANCE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Applicability & Scope

- **Regulatory Context:** Infer which frameworks may apply from the data and business model, and list assumptions; do not provide legal conclusions.
- **Data Classification:** Identify regulated data types (cardholder, health, personal, financial).
- **Control Inventory:** Map existing technical and procedural controls to framework requirements.
- Distinguish technical findings from items needing organizational evidence.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Audit Trails & Accountability

- **Event Coverage:** Check logging of authentication, authorization changes, data access, admin actions, and configuration changes.
- **Attribution:** Check that events identify actor, time, target, and outcome.
- **Integrity & Retention:** Check tamper resistance, retention length, and access to logs.
- **Reconstruction:** Test whether an important business change can be reconstructed from records.

## 3. Policy Enforcement

- **Access Control:** Check least privilege, reviews, and segregation of duties as enforced by code.
- **Change Management:** Check review requirements, approvals, and traceability from change to deployment.
- **Data Handling:** Check encryption, masking, and prohibited-data rules in practice.
- **Retention & Deletion:** Check enforcement of retention schedules.
- **Third-Party Controls:** Check vendor data-sharing and contractual-control evidence.

## 4. Control Gaps

- **Documented vs. Implemented:** Find policies without technical enforcement.
- **Implemented vs. Evidenced:** Find controls that exist but leave no audit evidence.
- **Exceptions:** Find undocumented bypasses, shared accounts, and emergency access.
- **Incident & Breach Readiness:** Check detection, response, and notification capability.

## 5. Remediation & Audit Readiness

- **Risk Ranking:** Rank gaps by regulatory exposure and likelihood.
- **Evidence Plan:** List the artifacts an auditor would request and their availability.
- **Roadmap:** Sequence remediation toward audit readiness.

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
