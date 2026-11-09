# Comprehensive Membership Lifecycle & Entitlements Audit

Act as a membership systems architect, subscription lifecycle specialist, and entitlement modeling expert conducting an exhaustive, production-grade membership and subscription lifecycle audit of this repository and everything it deploys, configures, or depends on.

Review signup, onboarding, plans and tiers, renewals, trials, upgrades and downgrades, suspension, cancellation, reactivation, entitlements, access gating, and related notifications and admin tools.

Your objective is to identify **lifecycle gaps, incorrect entitlement decisions, bad account state transitions, renewal and cancellation defects, access that outlives or precedes payment, and inconsistent membership status across components**.

Evaluate the system against mature, current industry standards (subscription state machine modeling, entitlement-based access design, and grace-period and dunning best practices), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `MEMBERSHIP_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Membership Model Inventory

- **Entities:** Identify members, accounts, organizations, plans, subscriptions, and entitlements.
- **Status Model:** Document every membership state and which fields define it.
- **Sources of Truth:** Determine whether status is stored, derived, or synced from a billing provider.
- **Plan Catalogue:** Document tiers, limits, add-ons, and legacy plans.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Signup & Onboarding

- **Registration:** Check verification, duplicate accounts, and invitation handling.
- **Trial Logic:** Check trial start, end, conversion, and repeat-trial prevention.
- **Onboarding Completeness:** Check the path from signup to first value.
- **Abandoned Signups:** Check cleanup and re-engagement of incomplete accounts.

## 3. Renewals, Changes & Cancellation

- **Renewal Handling:** Check scheduling, failure, retry, and grace periods.
- **Upgrades & Downgrades:** Check proration, timing, immediate versus end-of-term effect, and limit enforcement after downgrade.
- **Cancellation:** Check access until period end, data retention, and confirmation.
- **Pause & Suspension:** Check reasons, effects, and resumption.
- **Reactivation:** Check restoring state, data, and pricing.
- **Account Transitions:** Check ownership transfer, merges, and member removal.

## 4. Entitlements & Access

- **Entitlement Derivation:** Check that access derives from a single, correct computation of plan and status.
- **Enforcement Consistency:** Check gating in UI, API, background jobs, and exports.
- **Stale Access:** Check access persisting after expiry or revocation due to caching or tokens.
- **Premature Access:** Check access granted before payment confirmation.
- **Limits & Quotas:** Check seat counts, usage caps, and overage behavior.

## 5. Edge Cases & Remediation

- **Race Conditions:** Check simultaneous renewal, cancellation, and upgrade.
- **Time Handling:** Check time zones, anniversary dates, and month-end renewals.
- **Admin Overrides:** Check manual adjustments and their audit trail.
- **Communications:** Check renewal reminders, receipts, failure, and cancellation emails.
- **Prioritized Fixes:** Rank by revenue leakage and member harm.

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
