# Comprehensive Site Reliability, Availability & Resilience Audit

Act as a principal site reliability engineer (SRE), incident commander, and resilience architect conducting an exhaustive, production-grade reliability and availability audit of this repository and everything it deploys, configures, or depends on.

Review application runtime behavior, deployment topology, health checks, scaling, dependency handling, error budgets, runbooks, on-call tooling, and incident-related documentation.

Your objective is to identify **single points of failure, missing or unrealistic SLOs, poor failure recovery, absent graceful degradation, unsafe dependencies, capacity risks, and gaps in incident readiness**.

Evaluate the system against mature, current industry standards (Google SRE practices, SLO/error-budget methodology, and production readiness review criteria), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `RELIABILITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Service Inventory & Criticality

- **User Journeys:** Identify critical user-facing paths and their dependencies.
- **Dependency Map:** List internal and third-party dependencies and what happens when each fails.
- **Service Tiers:** Determine which components are critical, important, or best-effort.
- **Deployment Topology:** Document regions, zones, instance counts, and redundancy.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. SLOs & Measurement

- **Defined Objectives:** Are availability and latency SLOs defined, and are they tied to user experience?
- **Indicators:** Are SLIs actually measurable from existing telemetry?
- **Error Budgets:** Is there a policy governing releases when budgets are exhausted?
- **Alerting Linkage:** Do alerts map to SLO burn rather than arbitrary thresholds?
- Do not invent SLO targets; recommend how to derive them.

## 3. Failure Modes & Graceful Degradation

- **Single Points of Failure:** Identify components without redundancy.
- **Dependency Failure:** Define behavior for each dependency outage; check timeouts, retries, and circuit breakers.
- **Degraded Modes:** Can the system serve partial functionality?
- **Retry Storms & Overload:** Check backpressure, load shedding, and queue bounds.
- **Health Checks:** Distinguish liveness from readiness and check for misleading checks.
- **Startup & Shutdown:** Check graceful termination, connection draining, and cold-start behavior.

## 4. Capacity, Scaling & Resource Limits

- **Autoscaling:** Evaluate triggers, limits, and scale-up latency.
- **Resource Limits:** Check CPU/memory limits, file descriptors, and connection caps.
- **Growth Headroom:** Identify components approaching practical limits.
- **Statefulness:** Find state that prevents horizontal scaling or safe restarts.
- **Thundering Herd:** Check cache stampedes and synchronized schedulers.

## 5. Incident Readiness

- **Runbooks:** Are procedures present, actionable, and current for likely failures?
- **Detection:** Would an outage be noticed before users report it?
- **Rollback & Mitigation:** Can a bad release or config be reverted quickly?
- **On-Call Support:** Evaluate escalation paths, dashboards, and diagnostic access.
- **Postmortem Practice:** Look for evidence of learning from past incidents.
- **Chaos & Game Days:** Identify untested failure assumptions.

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
