# Comprehensive Observability, Logging & Diagnostics Audit

Act as an observability architect, telemetry engineer, and incident diagnostics specialist conducting an exhaustive, production-grade observability audit of this repository and everything it deploys, configures, or depends on.

Review application logging, metrics, tracing, health endpoints, dashboards, alert definitions, error reporting, correlation identifiers, and the instrumentation libraries and pipelines in use.

Your objective is to identify **blind spots, noisy or insufficient logs, missing metrics, broken trace propagation, weak alerting, sensitive data in telemetry, and gaps that would slow diagnosis of production incidents**.

Evaluate the system against mature, current industry standards (OpenTelemetry conventions, the three pillars of observability, RED and USE metrics, and SLO-based alerting), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `OBSERVABILITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Telemetry Inventory

- **Signals:** Identify logs, metrics, traces, events, and error tracking in use.
- **Tooling:** Identify vendors, agents, collectors, and retention.
- **Coverage Map:** Determine which services and paths are instrumented and which are dark.
- **Ownership:** Determine who maintains dashboards and alerts.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Logging Quality

- **Structure:** Are logs structured, leveled, and consistently formatted?
- **Context:** Do logs carry request, user, tenant, and correlation identifiers?
- **Signal vs. Noise:** Find log spam, duplicate logging of the same error, and missing logs on failure paths.
- **Sensitive Data:** Find secrets, tokens, PII, and full payloads logged.
- **Volume & Cost:** Identify high-cardinality or excessive logging.

## 3. Metrics & Tracing

- **Golden Signals:** Are latency, traffic, errors, and saturation measured?
- **Business Metrics:** Are key domain outcomes (signups, payments, jobs) tracked?
- **Cardinality:** Find unbounded label values.
- **Trace Propagation:** Are context headers passed through HTTP, queues, and background jobs?
- **Span Quality:** Check naming, attributes, sampling strategy, and error recording.
- **Dependency Visibility:** Are database, cache, and third-party calls visible?

## 4. Alerting & Diagnostics

- **Alert Quality:** Are alerts actionable, symptom-based, and tied to runbooks?
- **Alert Gaps:** Which realistic failures would trigger no alert?
- **Alert Noise:** Identify flapping, duplicate, or ignored alerts.
- **Error Tracking:** Check grouping, release tagging, and source maps.
- **Dashboards:** Assess whether they answer operational questions quickly.
- **Health Checks:** Check meaningfulness beyond returning 200.

## 5. Incident Walkthroughs

- **Simulate Diagnosis:** For several plausible failures, trace how an engineer would detect, locate, and confirm the cause with existing telemetry.
- **Identify Missing Data:** Name the exact signal that would have shortened each walkthrough.
- **Retention & Access:** Verify that data survives long enough and is accessible during incidents.

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
