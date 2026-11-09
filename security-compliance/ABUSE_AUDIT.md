# Comprehensive Abuse Prevention, Fraud & Resource Exhaustion Audit

Act as an abuse prevention engineer, fraud analyst, and adversarial thinking specialist conducting an exhaustive, production-grade abuse and fraud prevention audit of this repository and everything it deploys, configures, or depends on.

Review public and authenticated endpoints, registration, login, password reset, invitations, referral and promotion flows, payments, messaging, file uploads, search, exports, and any resource-consuming operations.

Your objective is to identify **workflow abuse, account enumeration, credential stuffing exposure, automated attacks, rate-limit bypasses, resource exhaustion, promotion or trial abuse, and economic denial-of-service**.

Evaluate the system against mature, current industry standards (OWASP Automated Threats to Web Applications, API4 Unrestricted Resource Consumption, and threat modeling (STRIDE)), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `ABUSE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Abuse Surface Inventory

- **Abusable Actions:** List every action that costs money, sends messages, creates records, or consumes compute.
- **Adversary Profiles:** Consider spammers, scrapers, fraudsters, competitors, and malicious insiders.
- **Incentives:** Identify what an attacker gains from each flow.
- Reason from code and configuration only; do not run attacks.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Account & Identity Abuse

- **Enumeration:** Find differing responses, timing, or messages revealing whether accounts exist.
- **Credential Stuffing:** Check lockouts, rate limits, breach-password checks, and bot defenses.
- **Mass Signup:** Check verification, disposable emails, and CAPTCHA coverage.
- **Invitation & Referral Abuse:** Check self-referral, loops, and unlimited invitations.
- **Trial & Promotion Abuse:** Check re-registration to obtain repeated benefits and coupon reuse.

## 3. Rate Limiting & Throttling

- **Coverage:** Find unthrottled endpoints, especially authentication, search, and messaging.
- **Bypass:** Check limits keyed on spoofable headers, per-IP only, or per-instance counters.
- **Granularity:** Check per-user, per-tenant, and global limits.
- **Distributed Attackers:** Check effectiveness against many IPs.
- **Response Behavior:** Check lockout abuse that lets attackers deny service to victims.

## 4. Resource Exhaustion

- **Unbounded Inputs:** Find missing limits on payload size, array length, query depth, pagination, and upload size.
- **Expensive Operations:** Find endpoints triggering heavy queries, exports, or third-party charges.
- **Amplification:** Find emails/SMS triggered by anonymous users and notification fan-out.
- **Queue & Storage Flooding:** Check job queue and storage quotas.
- **Regex and Parser DoS:** Check expensive parsing of untrusted data.

## 5. Business Logic & Detection

- **Workflow Manipulation:** Find step skipping, replay, race-based double-spend, and price or quantity tampering.
- **Detection:** Check anomaly signals, abuse logging, and alerting.
- **Response Tools:** Check ability to block, suspend, and reverse abuse.
- **Prioritized Mitigations:** Rank by attacker gain and cost to the business.

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
