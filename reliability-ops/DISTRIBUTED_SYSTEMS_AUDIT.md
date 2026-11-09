# Comprehensive Distributed Systems, Concurrency & Failure-Handling Audit

Act as a principal distributed systems architect, senior concurrency specialist, and resilience engineer conducting an exhaustive, production-grade distributed systems correctness audit of this repository and everything it deploys, configures, or depends on.

Review service-to-service communication, queues and event streams, background workers, schedulers, caches, locks, retries, timeouts, sagas, and every workflow spanning more than one process or datastore.

Your objective is to identify **race conditions, lost or duplicated messages, inconsistent state across components, unsafe retries, cascading failures, split-brain risks, ordering assumptions, and missing failure handling**.

Evaluate the system against mature, current industry standards (the fallacies of distributed computing, CAP/PACELC tradeoffs, idempotent-consumer and outbox patterns, saga design, and at-least-once delivery semantics), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DISTRIBUTED_SYSTEMS_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Topology & Communication Inventory

- **Components:** Identify services, workers, brokers, caches, and external dependencies.
- **Communication Styles:** Classify synchronous calls, async messaging, polling, webhooks, and shared-database coupling.
- **Delivery Guarantees:** Determine at-most-once, at-least-once, or exactly-once expectations versus actual behavior.
- **Consistency Model:** Identify where strong, eventual, or no consistency is assumed.
- Trace key workflows end to end across component boundaries.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Concurrency & Race Conditions

- **Check-Then-Act:** Find decisions made on stale state before writing.
- **Duplicate Submission:** Find workflows where simultaneous identical requests create duplicate effects.
- **Lost Updates:** Find concurrent writers overwriting each other without version checks.
- **Worker Contention:** Find jobs and handlers competing for the same records without leasing or locking.
- **Distributed Locks:** Evaluate lock scope, expiry, fencing tokens, and release on failure.
- **Clock Assumptions:** Find logic that depends on synchronized wall clocks or timestamp ordering.

## 3. Messaging, Retries & Idempotency

- **Idempotent Consumers:** Can redelivered messages repeat side effects?
- **Ordering:** Which consumers break under reordered or concurrent processing?
- **Dual Writes:** Find places where a database write and a message publish can diverge; check for an outbox.
- **Retry Policy:** Check backoff, jitter, caps, and retry of non-idempotent calls.
- **Dead Letters & Poison Messages:** Check handling, visibility, and replay safety.
- **Compensation:** Evaluate saga rollback and reconciliation for partial failures.

## 4. Failure Propagation & Resilience

- **Timeouts:** Are every remote call and queue wait bounded?
- **Cascading Failure:** Identify retry storms, unbounded queues, and thundering herds.
- **Circuit Breaking & Bulkheads:** Is one failing dependency able to exhaust shared resources?
- **Backpressure:** Does the system shed or slow load, or collapse?
- **Graceful Degradation:** Define behavior when each dependency is down.
- **Partial Failure:** Identify workflows left half-complete with no recovery path.

## 5. Verification & Observability

- **Distributed Tracing:** Can a request be followed across components?
- **Reconciliation:** Are there jobs that detect and repair divergent state?
- **Failure Testing:** Identify missing chaos, fault-injection, or concurrency tests.
- Label each finding as a confirmed race or a risk requiring integration or load testing.

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
