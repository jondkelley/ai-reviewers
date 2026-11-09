# Comprehensive Identity, Access Management & Authorization Model Audit

Act as an identity and access management architect, authorization model specialist, and privilege escalation analyst conducting an exhaustive, production-grade identity and access management audit of this repository and everything it deploys, configures, or depends on.

Review user and service identities, roles, permissions, policies, group and organization hierarchies, session and token lifecycle, SSO and OAuth integrations, API keys, admin tooling, and infrastructure-level IAM definitions.

Your objective is to identify **privilege escalation paths, permission inheritance flaws, excessive access, orphaned accounts, weak session lifecycle controls, insecure account recovery, and inconsistent authorization enforcement**.

Evaluate the system against mature, current industry standards (least privilege, separation of duties, NIST SP 800-63 and 800-53 access control families, OAuth 2.0/OIDC security best practices, and zero-trust principles), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `IAM_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Identity & Permission Inventory

- **Identity Types:** Catalogue human users, service accounts, API keys, and machine tokens.
- **Role Model:** Document roles, permissions, groups, and tenant or organization scoping.
- **Enforcement Points:** Locate every place authorization is evaluated and compare for consistency.
- **Source of Truth:** Determine where roles and permissions are defined and whether they can diverge.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Authorization Model Correctness

- **Role Design:** Find roles that are overly broad, overlapping, or unused.
- **Permission Inheritance:** Check hierarchy, group, and organization inheritance for unintended grants.
- **Privilege Escalation:** Find paths where a user can grant themselves or others more access.
- **Separation of Duties:** Check that conflicting powers (approve and request, create and audit) are separated.
- **Tenant Boundaries:** Check cross-tenant leakage and super-admin scoping.
- **Default Permissions:** Check defaults for new users, invitations, and imported accounts.

## 3. Session & Token Lifecycle

- **Issuance & Expiry:** Check lifetimes, refresh rotation, and idle timeouts.
- **Revocation:** Check logout, password change, role change, and account suspension invalidating existing sessions and tokens.
- **Stale Claims:** Check cached roles in tokens that outlive permission changes.
- **Concurrent Sessions & Devices:** Check visibility and control.
- **API Keys:** Check scoping, rotation, hashing at rest, and last-used tracking.

## 4. Account Lifecycle & Recovery

- **Provisioning & Deprovisioning:** Check onboarding, offboarding, and orphaned accounts.
- **Account Recovery:** Check reset flows, support-assisted recovery, and social engineering exposure.
- **MFA:** Check enrollment, recovery codes, and downgrade or bypass paths.
- **Impersonation:** Check admin impersonation controls and audit.
- **SSO/OAuth:** Check redirect URI validation, state/PKCE, account linking takeover, and just-in-time provisioning.

## 5. Governance & Audit

- **Access Reviews:** Check mechanisms for periodic recertification.
- **Audit Trails:** Check that grants, revocations, and privileged actions are attributable.
- **Break-Glass Access:** Check emergency access controls and monitoring.
- **Remediation:** Rank by escalation severity and propose a least-privilege target model.

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
