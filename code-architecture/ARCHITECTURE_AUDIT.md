# Comprehensive Architecture, Coupling & Technical Debt Audit

Act as a principal software architect, senior systems designer, and technical-debt analyst conducting an exhaustive, production-grade software architecture audit of this repository and everything it deploys, configures, or depends on.

Review the entire codebase structure, module and service boundaries, dependency graph, layering, shared libraries, configuration, build setup, and architectural documentation.

Your objective is to identify **architectural inconsistencies, harmful coupling, weak cohesion, leaky abstractions, boundary violations, circular dependencies, and compounding technical debt**.

Evaluate the system against mature, current industry standards (clean/hexagonal architecture, domain-driven design, SOLID, evolutionary architecture), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `ARCHITECTURE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Architecture Inventory & Reality Check

- **Components:** Identify every service, module, package, worker, and deployable unit and its responsibility.
- **Dependency Direction:** Map which components depend on which, and compare against any documented architecture.
- **Layering:** Determine whether presentation, domain, and persistence concerns are separated or interleaved.
- **Entry Points:** Catalogue HTTP, CLI, queue, cron, and webhook entry points and where they converge.
- **Sources of Truth:** Identify duplicated or competing definitions of the same concept.
- **Documentation Drift:** Note where ADRs, diagrams, or READMEs contradict the code.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Coupling & Cohesion

- **Circular Dependencies:** Locate import cycles between modules or packages.
- **God Modules:** Identify files, classes, or services that accumulate unrelated responsibilities.
- **Shotgun Surgery:** Find concepts that require edits in many places to change.
- **Feature Envy:** Find logic that manipulates another module's data more than its own.
- **Shared Mutable State:** Identify globals, singletons, and shared caches that couple unrelated code.
- **Temporal Coupling:** Find operations that only work if called in an undocumented order.

## 3. Boundaries & Abstractions

- **Service Boundaries:** Are boundaries aligned with business capabilities and data ownership?
- **Leaky Abstractions:** Do implementation details (ORM entities, vendor SDK types, transport formats) escape their layer?
- **Premature Abstraction:** Identify interfaces, factories, and plugin systems with a single implementation and no demonstrated need.
- **Missing Abstraction:** Identify repeated external integrations or policies scattered without a seam.
- **Public Surface:** Are internal modules importable by unrelated code with no enforced visibility?
- **Cross-Cutting Concerns:** Are logging, auth, config, and error handling applied consistently or reinvented per module?

## 4. Evolvability & Change Risk

- **Change Hotspots:** Identify areas where change is risky, slow, or poorly tested.
- **Extension Points:** Evaluate how hard it is to add a new feature, tenant, provider, or role.
- **Configuration Architecture:** Are environment differences handled through explicit configuration or scattered conditionals?
- **Build & Module Structure:** Evaluate monorepo/package layout, build times, and dependency hygiene.
- **Distributed Monolith Signals:** Identify services that must deploy or fail together.

## 5. Technical Debt Register

- **Debt Inventory:** List TODO/FIXME/HACK markers, workarounds, and deferred decisions with their consequences.
- **Debt Interest:** Rank debt by how much it slows or endangers ongoing work.
- **Dead Architecture:** Identify abandoned subsystems, half-finished migrations, and parallel old/new implementations.
- **Strategic Recommendations:** Propose incremental refactors, avoiding big-bang rewrites.

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
