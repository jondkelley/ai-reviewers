# Comprehensive Concurrency, Race Condition & Lost Write Audit

Act as a concurrency testing engineer, race condition hunter, and parallel systems reviewer conducting an exhaustive, production-grade concurrency audit of this repository and everything it deploys, configures, or depends on.

Review request handlers, background workers, scheduled jobs, shared in-memory state, caches, database write paths, file access, and client-side state updates that can interleave.

Your objective is to identify **race conditions, duplicate submissions, simultaneous update conflicts, lost writes, double processing, unsafe shared state, deadlocks, and missing concurrency tests**.

Evaluate the system against mature, current industry standards (linearizability reasoning, happens-before analysis, optimistic and pessimistic concurrency control, and idempotency design), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `CONCURRENCY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Shared State Inventory

- **Shared Resources:** Identify rows, files, caches, counters, queues, and in-memory objects accessed by multiple actors.
- **Actors:** Identify concurrent actors (requests, workers, cron, users, multiple instances, browser tabs).
- **Runtime Model:** Document threading, async, process, and multi-instance behavior.
- **Mutation Points:** List every writer for each critical resource.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Check-Then-Act & Read-Modify-Write

- **Stale Decisions:** Find decisions based on data that may change before the write.
- **Counters & Balances:** Find increments and decrements done in application code instead of atomically.
- **Uniqueness & Capacity:** Find limits (seats, stock, quotas, usernames) enforced by prior reads.
- **Lost Updates:** Find updates that overwrite whole records using stale copies.
- **State Machines:** Find concurrent transitions that can both succeed.

## 3. Duplicate Submission & Idempotency

- **Double Click & Retry:** Find handlers that create duplicates on repeat requests.
- **Webhook & Message Redelivery:** Check duplicate-event handling.
- **Idempotency Keys:** Check generation, storage, and race-safe enforcement.
- **Client Safeguards:** Check disabled buttons are not the only protection.
- **Cross-Tab and Cross-Device Edits:** Check conflict detection.

## 4. Locking & Deadlock

- **Lock Granularity:** Check that locks cover the whole critical section, no more.
- **Lock Ordering:** Find inconsistent acquisition orders.
- **Distributed Locks:** Check expiry, ownership, and fencing.
- **Lock Duration:** Find locks held across I/O.
- **Worker Contention:** Check leasing and claim semantics for jobs.
- **In-Process Hazards:** Find unsynchronized shared maps, singletons, and memoization races.

## 5. Test Strategy

- **Reproduction Recipes:** For each race, describe an interleaving or parallel request script that would expose it.
- **Confirmed vs. Risk:** Separate races provable from code from those needing load or stress tests.
- **Proposed Tests:** Recommend concurrency tests and tooling for the top risks.
- **Fix Patterns:** Recommend unique constraints, conditional updates, row locks, versioning, or queues as appropriate.

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
