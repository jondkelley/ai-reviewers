# Comprehensive Payments, Billing & Financial Correctness Audit

Act as a payments and billing systems architect, financial reconciliation specialist, and payment integration security reviewer conducting an exhaustive, production-grade payments and billing audit of this repository and everything it deploys, configures, or depends on.

Review payment provider integrations, checkout flows, invoicing, subscription billing, taxes, discounts, refunds, credits, webhooks, ledgers, reconciliation jobs, and payout handling.

Your objective is to identify **duplicate or missed charges, incorrect amounts, billing state inconsistencies, webhook handling defects, refund and credit errors, reconciliation gaps, and financial data integrity risks**.

Evaluate the system against mature, current industry standards (double-entry bookkeeping principles, payment provider best practices, PCI DSS scope reduction, and idempotent financial operations), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `BILLING_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Billing Architecture Inventory

- **Providers:** Identify payment processors, tax services, and invoicing tools.
- **Flows:** Map one-time payments, subscriptions, invoicing, refunds, and payouts end to end.
- **Source of Truth:** Determine whether the provider or the local database is authoritative for each billing fact.
- **Card Data Handling:** Verify that raw card data never touches the application, and note PCI scope.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Money & Calculation Correctness

- **Representation:** Check integer minor units or decimals versus floats, and currency tracking.
- **Rounding:** Check rounding location, mode, and consistency between totals and line items.
- **Tax, Discounts, Proration:** Check calculation order and edge cases.
- **Currency & FX:** Check conversion handling and mixed-currency arithmetic.
- **Price Tampering:** Check that amounts are computed server-side.

## 3. Charge Integrity & Idempotency

- **Duplicate Charges:** Check idempotency keys, double-click, and retry safety.
- **Failed Payments:** Check retry schedules, dunning, and state after failure.
- **Partial Failure:** Check divergence between provider charge and local record.
- **Authorization vs. Capture:** Check handling of holds, expiry, and voids.
- **Concurrency:** Check simultaneous charges, credits, and balance changes.

## 4. Webhooks & Reconciliation

- **Signature Verification:** Check authenticity validation.
- **Idempotent Handling:** Check duplicate and out-of-order events.
- **Missed Events:** Check replay and polling fallback.
- **Event Coverage:** Check handling of disputes, chargebacks, refunds, and failed renewals.
- **Reconciliation:** Check automated comparison of local records against provider and bank data.
- **Ledger Integrity:** Check immutability, balancing, and auditability of financial records.

## 5. Refunds, Disputes & Reporting

- **Refund Logic:** Check partial refunds, over-refund prevention, and entitlement reversal.
- **Credits & Adjustments:** Check authorization and audit trail.
- **Disputes:** Check evidence retention and status handling.
- **Financial Reporting:** Check accuracy of revenue, tax, and outstanding balance reports.
- **Prioritized Risks:** Rank by potential financial loss and customer harm.

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
