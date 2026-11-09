# Comprehensive Cloud Infrastructure, Networking & Environment Audit

Act as a cloud infrastructure architect, network engineer, and infrastructure-as-code reviewer conducting an exhaustive, production-grade cloud infrastructure audit of this repository and everything it deploys, configures, or depends on.

Review Terraform/Pulumi/CloudFormation/Bicep, Kubernetes manifests, Helm charts, Dockerfiles, compose files, networking, DNS, load balancers, storage, IAM bindings at the infrastructure level, and environment definitions.

Your objective is to identify **topology weaknesses, misconfigured networking, over- or under-provisioned resources, environment inconsistencies, configuration drift, insecure defaults, and fragile infrastructure definitions**.

Evaluate the system against mature, current industry standards (the Well-Architected frameworks of the cloud providers in use, CIS benchmarks, and infrastructure-as-code best practices), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `INFRASTRUCTURE_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Infrastructure Inventory

- **Provider & Services:** Identify cloud providers, regions, and managed services in use.
- **Infrastructure as Code:** Determine what is codified versus created manually, and state management.
- **Environments:** Identify dev, staging, and production definitions and how they relate.
- **Workload Placement:** Document compute type, containers, serverless, and scheduling.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Network Topology

- **Segmentation:** Evaluate VPCs, subnets, public versus private placement, and security groups.
- **Ingress & Egress:** Review exposed ports, load balancers, WAF, CDN, and outbound controls.
- **DNS & TLS:** Check records, certificate management, and expiry risk.
- **Service Connectivity:** Review private endpoints, peering, and cross-zone traffic.
- **Overly Permissive Rules:** Flag wide-open CIDRs and unrestricted administrative access.

## 3. Resource Allocation & Configuration

- **Sizing:** Identify resources without evidence-based requests and limits.
- **Storage:** Review volume types, lifecycle, encryption, and growth.
- **Defaults:** Flag unsafe or implicit provider defaults.
- **Tagging & Ownership:** Check resource tagging, naming, and ownership clarity.
- **Container Images:** Check base images, pinned versions, user privileges, and layer hygiene.
- **Kubernetes:** Review probes, resource limits, disruption budgets, affinity, and secrets handling when applicable.

## 4. Environment Consistency & Drift

- **Parity:** Identify differences between environments that hide production-only bugs.
- **Drift Detection:** Is there a way to detect manual changes?
- **Configuration Management:** Review variable handling, secrets, and per-environment overrides.
- **Reproducibility:** Can an environment be rebuilt from code alone?
- **Module Reuse:** Identify copy-pasted infrastructure definitions.

## 5. Operability & Change Safety

- **Plan Review:** Is infrastructure change reviewed through plan output before apply?
- **Blast Radius:** Evaluate state partitioning and destructive-change protections.
- **Lifecycle Protections:** Check deletion protection and prevent_destroy on critical resources.
- **Documentation:** Check diagrams and runbooks for accuracy against code.

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
