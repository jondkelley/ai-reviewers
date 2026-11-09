# Comprehensive Application Security Audit

Act as a principal application security engineer, penetration-testing lead, and secure code reviewer conducting an exhaustive, production-grade application security audit of this repository and everything it deploys, configures, or depends on.

Review all source code, configuration, authentication and session handling, authorization checks, input handling, output encoding, file handling, secrets, third-party integrations, and security headers.

Your objective is to identify **authentication and authorization flaws, injection, cross-site scripting, CSRF, SSRF, insecure deserialization, secrets exposure, insecure defaults, and other exploitable implementation weaknesses**.

Evaluate the system against mature, current industry standards (OWASP Top 10, OWASP ASVS, CWE Top 25, and secure-by-default design), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `SECURITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Attack Surface Inventory

- **Entry Points:** Enumerate routes, webhooks, file uploads, queues, CLIs, and admin interfaces.
- **Trust Boundaries:** Identify where untrusted data enters and where privilege changes.
- **Data Sensitivity:** Identify credentials, PII, financial and health data, and where each flows.
- Do not exploit anything or run active attacks; reason from code and configuration.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Authentication & Session Management

- **Credential Handling:** Check password hashing, strength rules, and secure storage.
- **Login Flow:** Check brute-force protection, enumeration leakage, and MFA.
- **Sessions & Tokens:** Check generation entropy, expiry, rotation, revocation, cookie flags, and JWT validation (algorithm, audience, expiry).
- **Password Reset & Recovery:** Check token single-use, expiry, and enumeration.
- **Secrets in Code:** Find hard-coded keys, tokens, and credentials, including in history and examples.

## 3. Authorization & Access Control

- **Object-Level:** Find endpoints that fetch records by ID without ownership or tenant checks (IDOR/BOLA).
- **Function-Level:** Find privileged actions callable by lower roles.
- **Mass Assignment:** Find request bodies bound directly to models.
- **Default-Deny:** Check whether new routes are protected by default.
- **Client-Side Trust:** Find authorization decisions enforced only in the UI.

## 4. Injection & Input Handling

- **SQL/NoSQL/Command Injection:** Find string-built queries and shell invocations with user data.
- **XSS:** Find unescaped output and unsafe HTML sinks.
- **CSRF & CORS:** Check token use, SameSite, and origin policy.
- **SSRF & Open Redirect:** Find user-controlled URLs fetched or redirected to.
- **File Handling:** Check upload validation, path traversal, and storage location.
- **Deserialization & Templates:** Find unsafe parsing and server-side template injection.
- **Redirect, XXE, and Regex DoS:** Check parsers and patterns on untrusted data.

## 5. Configuration, Transport & Hardening

- **Security Headers:** Check CSP, HSTS, X-Content-Type-Options, and framing protections.
- **TLS & Crypto:** Find weak algorithms, homemade crypto, static IVs, and insecure randomness.
- **Error Disclosure:** Find stack traces and verbose errors exposed to users.
- **Debug & Default Settings:** Find debug modes and default credentials in production paths.
- **Logging of Secrets:** Cross-reference secrets and PII in logs.

## 6. Findings Quality

- **Exploitability:** For each finding describe the attacker, preconditions, and impact; rate realistically.
- **Remediation:** Provide specific, secure code-level fixes.
- **Defense in Depth:** Recommend compensating controls where fixes are not immediate.

## 7. Evidence Standards & Calibration

- **Cite Evidence:** Every finding must reference concrete files, lines, configuration, queries, or observed behavior. Never fabricate evidence, metrics, or benchmarks.
- **Confirmed vs. Suspected:** Clearly label each finding as Confirmed (demonstrable from the code or configuration) or Risk (requires runtime, load, or environment verification).
- **Repository Limits:** Do not claim a control is absent merely because it is not visible in the repository. Report missing operational evidence separately.
- **No Name-Based Guessing:** Do not infer a defect solely from a file, variable, or column name.
- **Concrete Scenarios:** For each finding, describe the specific input, state, or sequence of events that produces the failure and who or what is harmed.
- **Acknowledge Strengths:** Record practices that are done well so they are preserved.

## 8. Required Report Structure

1. **Executive Summary:** Overall posture, the highest-impact risks, and a one-paragraph verdict.
2. **Inventory & Scope:** What was reviewed, what was not, and the assumptions made.
3. **Findings:** Each with ID, title, severity (Critical / High / Medium / Low / Informational), confidence, location, evidence, concrete failure scenario, impact, and recommended fix.
4. **Quick Wins:** Low-effort, high-value changes.
5. **Remediation Roadmap:** Prioritized phases with dependencies and rough effort (S/M/L).
6. **Verification Plan:** How each fix should be tested or measured once implemented.
7. **Open Questions:** Information needed from the team to close remaining uncertainty.
