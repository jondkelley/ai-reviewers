# Comprehensive Business Process & Workflow Lifecycle Audit

Act as a business process analyst, operations workflow designer, and process automation consultant conducting an exhaustive, production-grade business workflow audit of this repository and everything it deploys, configures, or depends on.

Review implemented business processes, status models, approval flows, notifications, background automation, manual steps implied by the product, and administrative tooling.

Your objective is to identify **workflow gaps, unnecessary manual work, approval bottlenecks, incomplete lifecycle handling, stuck or orphaned items, missing escalation, and process inconsistencies**.

Evaluate the system against mature, current industry standards (BPMN-style process analysis, lean process principles, and lifecycle completeness analysis), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `WORKFLOW_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Process Inventory

- **Business Processes:** Identify processes the software supports (onboarding, approvals, fulfillment, support, renewals).
- **Actors & Roles:** Identify who initiates, approves, and observes each step.
- **Process Maps:** Reconstruct each workflow as steps, decisions, and states from the code.
- State your assumptions about business intent explicitly.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Lifecycle Completeness

- **Start-to-End Coverage:** Verify that each entity can move through its entire intended lifecycle.
- **Exception Paths:** Check cancellation, rejection, reversal, expiry, and failure handling.
- **Stuck Items:** Find states from which no transition exists or that wait on events that may never occur.
- **Orphans:** Find records whose parent workflow ended or was deleted.
- **Timeouts & Escalation:** Check handling of items awaiting action indefinitely.

## 3. Manual Work & Bottlenecks

- **Manual Steps:** Find tasks staff must do outside the system or by database edit.
- **Approval Chains:** Find single-approver bottlenecks and missing delegation.
- **Data Re-entry:** Find duplicated entry across screens or systems.
- **Batch Needs:** Find repetitive individual actions that need bulk handling.
- **Visibility:** Check whether stakeholders can see where an item is.

## 4. Automation & Notifications

- **Triggers:** Check automated transitions, schedules, and reminders for correctness.
- **Notification Gaps:** Find events nobody is told about, and noisy duplicates.
- **Idempotency of Automation:** Check retries of automated steps.
- **Failure Handling:** Check what happens when automation fails midway.
- **Auditability:** Check that process history can be reconstructed.

## 5. Improvements

- **Process Gaps by Impact:** Rank by operational cost and risk.
- **Target Workflow:** Propose simplified flows for the worst offenders.
- **Metrics:** Recommend cycle time, backlog, and error measures.

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
