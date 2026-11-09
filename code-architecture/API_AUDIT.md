# Comprehensive API Design, Contract & Consistency Audit

Act as a principal API architect, senior platform engineer, and API governance specialist conducting an exhaustive, production-grade API design and contract audit of this repository and everything it deploys, configures, or depends on.

Review every public, internal, and third-party-facing API, including REST/GraphQL/RPC endpoints, OpenAPI or schema definitions, request validation, error handling, versioning, authentication integration, SDKs, and webhooks.

Your objective is to identify **inconsistent conventions, contract violations, unsafe or ambiguous semantics, missing validation, weak error contracts, pagination defects, versioning risks, and idempotency failures**.

Evaluate the system against mature, current industry standards (REST maturity guidance, RFC 9110 HTTP semantics, RFC 9457 problem details, OpenAPI, JSON:API conventions, Google/Microsoft API design guides), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `API_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. API Inventory & Contract Sources

- **Endpoint Catalogue:** List every route, method, and handler, including undocumented and internal ones.
- **Contract Sources:** Determine whether OpenAPI/GraphQL schemas are authoritative, generated, hand-written, or stale.
- **Consumers:** Identify first-party, third-party, and mobile consumers and their upgrade constraints.
- **Documentation Drift:** Compare documented contracts with actual request/response behavior.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Resource Modeling & HTTP Semantics

- **Resource Naming:** Evaluate noun usage, pluralization, nesting depth, and casing consistency.
- **Method Semantics:** Are GET safe, PUT/DELETE idempotent, and POST used appropriately?
- **Status Codes:** Are 2xx/4xx/5xx codes accurate and consistent, or is 200 returned for failures?
- **Headers & Content Types:** Review content negotiation, caching headers, ETags, and Location headers.
- **Field Conventions:** Check casing, date/time formats, enum representation, null vs. absent, and money encoding.
- **Response Shape:** Are envelopes, collections, and nested objects consistent across endpoints?

## 3. Validation, Errors & Pagination

- **Input Validation:** Are types, ranges, lengths, and required fields validated at the boundary with clear failures?
- **Unknown Fields:** Are unexpected fields rejected, ignored, or silently persisted (mass assignment)?
- **Error Contract:** Is there a single, machine-readable error format with stable codes and no leaked internals?
- **Pagination:** Evaluate cursor vs. offset, stable ordering, max page size, and total-count cost.
- **Filtering & Sorting:** Check whitelisting, injection safety, and consistent parameter conventions.
- **Bulk Endpoints:** Assess partial-failure semantics and payload limits.

## 4. Safety, Idempotency & Concurrency

- **Idempotency Keys:** Can client retries duplicate payments, orders, or other side effects?
- **Optimistic Concurrency:** Are ETags or version fields used to prevent lost updates?
- **Rate Limiting & Quotas:** Are limits defined, communicated via headers, and consistent?
- **Long-Running Operations:** Are async jobs modeled with status resources rather than blocking requests?
- **Authorization Surface:** Cross-reference object-level and function-level authorization gaps without duplicating the full security audit.

## 5. Versioning & Evolution

- **Versioning Strategy:** Is there a clear scheme, and are breaking changes avoided or flagged?
- **Deprecation:** Are sunset policies, headers, and migration guidance provided?
- **Backward Compatibility:** Identify changes that would break existing clients.
- **Webhooks & Events:** Review payload versioning, signing, retry, ordering, and replay behavior.
- **Developer Experience:** Evaluate discoverability, examples, SDK parity, and error clarity.

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
