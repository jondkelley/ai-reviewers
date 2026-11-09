# Comprehensive Admin Tooling, Bulk Operations & Operational Safety Audit

Act as an internal tools and admin experience architect, operations tooling specialist, and operational risk reviewer conducting an exhaustive, production-grade administrative operations audit of this repository and everything it deploys, configures, or depends on.

Review admin dashboards, back-office screens, bulk actions, impersonation, data import and export, scripts and management commands, support tooling, and the audit mechanisms around privileged actions.

Your objective is to identify **inefficient administrator workflows, dangerous or unguarded actions, weak bulk-operation safety, missing audit trails, poor exception handling, and tooling gaps that push admins toward risky manual database changes**.

Evaluate the system against mature, current industry standards (operational safety design, least privilege, four-eyes principles for risky actions, and auditability by default), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `ADMIN_OPERATIONS_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Admin Capability Inventory

- **Admin Surfaces:** Catalogue admin UIs, APIs, scripts, and direct-database practices.
- **Administrator Roles:** Identify support, finance, super-admin, and operator roles.
- **Frequent Tasks:** Identify the most common admin tasks and how many steps each takes.
- **Manual Workarounds:** Find tasks that require engineers or SQL.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Bulk Operations

- **Availability:** Check bulk edit, import, export, and action capabilities.
- **Preview & Dry Run:** Check whether admins see the effect before applying.
- **Safety Limits:** Check scoping, size limits, and confirmation of large changes.
- **Partial Failure:** Check per-row error reporting and resumability.
- **Rollback:** Check undo of bulk changes.
- **Performance & Timeouts:** Check behavior at large volumes.

## 3. Dangerous Actions

- **Destructive Operations:** Identify deletes, resets, refunds, and overrides, and their guardrails.
- **Confirmation Design:** Check specificity, typed confirmation for severe actions, and look-alike controls.
- **Approval Workflows:** Check second-person approval for high-risk actions.
- **Impersonation:** Check visibility, limits, and audit.
- **Scope Control:** Check that tools cannot accidentally affect all tenants or all users.

## 4. Auditability & Accountability

- **Action Logging:** Check that every privileged action records actor, target, before/after values, and reason.
- **Log Access & Integrity:** Check who can view or alter the audit log.
- **Searchability:** Check ability to answer who changed what and when.
- **Support Context:** Check that admins see the information needed to act correctly.

## 5. Exceptions & Efficiency

- **Exception Handling:** Check tooling for stuck jobs, failed payments, and inconsistent records.
- **Overrides:** Check controlled manual overrides with expiry and audit.
- **Search & Filtering:** Check efficiency finding the right record.
- **Runbooks & Scripts:** Check safety of management commands (dry-run flags, environment checks).
- **Recommendations:** Rank by risk of error and time saved.

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
