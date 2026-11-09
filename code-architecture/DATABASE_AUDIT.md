# Comprehensive Database Reliability, Integrity & Performance Audit

Act as a principal database reliability engineer (DBRE), senior database architect, database performance engineer, and distributed systems specialist conducting an exhaustive, production-grade database reliability, integrity, and performance audit of this repository and everything it deploys, configures, or depends on.

Review schema definitions, migrations, ORM models, raw SQL, query builders, data access layers, transactions, background jobs, caching, connection management, and application code that touches persistent data.

Your objective is to identify **schema integrity defects, missing or inefficient indexes, expensive queries, transaction anomalies, concurrency hazards, locking problems, migration risks, data consistency violations, inefficient persistence patterns, and operational reliability weaknesses**.

Evaluate the system against mature, current industry standards (ACID correctness, data durability, predictable performance, recoverability, and safe schema evolution), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `DATABASE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Persistence Architecture Inventory

- **Database Engines:** Identify every datastore (PostgreSQL, MySQL, SQLite, MongoDB, Redis, Firestore, etc.) and its role.
- **Ownership:** Determine which services and workers read or modify each store.
- **Connection Architecture:** Examine pools, proxies, managed services, and serverless connection handling.
- **ORM & Raw SQL:** Inventory ORMs, query builders, handwritten SQL, stored procedures, and dynamic query construction.
- **Schema Sources of Truth:** Determine whether migrations, declarative schemas, or ORM models are authoritative.
- **Cross-Store Consistency:** Identify workflows spanning multiple databases or persistence technologies.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Schema Design & Referential Integrity

- **Keys & Constraints:** Are primary keys, foreign keys, uniqueness, NOT NULL, and CHECK constraints enforced by the database rather than only by the application?
- **Referential Actions:** Are CASCADE, SET NULL, and RESTRICT rules consistent with business requirements?
- **Data Types:** Check money (no floats), timestamps and timezones, JSON, enums, and identifier types.
- **Normalization:** Identify update anomalies and duplicated facts, and over-normalization causing excessive joins.
- **Soft Deletes:** Determine whether soft-deleted rows break uniqueness, queries, retention, or referential integrity.
- **Orphans:** Identify paths that leave unreachable or inconsistent related rows.

## 3. Indexing & Query Performance

- **Missing Indexes:** Find filtered, joined, sorted, or grouped columns lacking support, based on actual query predicates.
- **Composite Order & Redundancy:** Evaluate column order and overlapping or unused indexes.
- **N+1 & Unbounded Queries:** Find loops that issue repeated queries and endpoints that fetch unlimited rows.
- **Sargability:** Find predicates that defeat indexes (functions on columns, leading wildcards, type mismatches).
- **Pagination & Aggregation:** Evaluate offset pagination, expensive sorts, and repeated aggregations.
- **Bulk Operations:** Find row-by-row processing that should be batched.
- **Write Amplification:** Identify excessive indexing that raises write cost.

## 4. Transactions, Concurrency & Locking

- **Atomicity:** Are related writes in one transaction, and can partial failure leave inconsistent state?
- **Isolation:** Are default isolation levels sufficient to prevent lost updates, write skew, and phantoms?
- **Read-Modify-Write Races:** Locate decisions made on read data and updated without locking or conditional writes.
- **Uniqueness Races:** Find check-then-insert patterns without a database constraint.
- **Inventory & Financial Invariants:** Can concurrent requests over-allocate capacity or double-process credits, refunds, or balances?
- **Deadlocks & Lock Order:** Identify inconsistent lock acquisition orders and long-held locks.
- **Transaction Scope:** Flag transactions held open across network calls or slow work, and unsafe retry behavior.
- Distinguish confirmed races from risks that require load testing.

## 5. Migrations, Consistency & Operations

- **Migration Safety:** Identify destructive changes, table rewrites, blocking DDL, non-concurrent index builds, unsafe NOT NULL additions, and unrestartable backfills; propose a safer expand-and-contract sequence.
- **Schema Drift & Rollback:** Assess ordering, drift detection, and realistic rollback.
- **Business Invariants:** Find rules enforced only in application code and bypassable by alternate write paths.
- **Idempotency & Events:** Check duplicate-effect risk from retries and out-of-order or repeated messages.
- **Pooling & Timeouts:** Evaluate pool sizing, leaks, statement and lock timeouts, and connection multiplication across instances.
- **Backup & Recovery:** Assess backups, PITR, restore testing, and RPO/RTO evidence; report missing operational evidence separately.
- **Observability:** Check slow query visibility, lock/deadlock diagnosis, long-running transaction detection, and replication lag monitoring.
- **Database Security:** Review least privilege, runtime DDL rights, tenant isolation, and credential handling.
- **Engine-Specific Concerns:** Apply only the concerns relevant to the engines actually in use (e.g., autovacuum and MVCC for PostgreSQL, gap locks for MySQL, WAL and busy timeouts for SQLite, shard keys for MongoDB, hotspots for Firestore, durability for Redis).

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
