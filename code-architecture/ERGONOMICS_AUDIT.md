# Comprehensive Human Factors, Cognitive Load & Operator Efficiency Audit

Act as a human factors and ergonomics engineer, cognitive psychologist, and operator workflow analyst conducting an exhaustive, production-grade human factors audit of this repository and everything it deploys, configures, or depends on.

Review forms, data entry, dashboards, repetitive workflows, administrative screens, confirmations, alerts, and any interface used for sustained or high-stakes work.

Your objective is to identify **excessive cognitive load, error-prone interactions, repetitive effort, form fatigue, poor error prevention, slow operator workflows, and designs that invite mistakes**.

Evaluate the system against mature, current industry standards (human error taxonomy, Fitts's and Hick's laws, error-prevention principles from ISO 9241, and cognitive load theory), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `ERGONOMICS_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Task & User Context

- **Operators:** Identify who uses each interface, how often, and under what pressure.
- **Task Frequency & Criticality:** Rank tasks by frequency and cost of error.
- **Environment:** Consider interruptions, multitasking, and device constraints.
- State clearly that conclusions derive from static review unless usage data exists.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Cognitive Load

- **Information Density:** Find screens presenting too much or too little at once.
- **Memory Demands:** Find tasks forcing users to remember values from another screen.
- **Decision Complexity:** Find choices with too many options or unclear criteria.
- **Progressive Disclosure:** Check whether advanced options are hidden until needed.
- **Consistency:** Check whether learned behaviors transfer across screens.

## 3. Error Prevention & Recovery

- **Constraint Design:** Prevent invalid input rather than reporting it afterward.
- **Slips vs. Mistakes:** Find easily mis-clicked adjacent actions and look-alike controls.
- **Confirmation Quality:** Check that confirmations are specific, not habituating.
- **Undo:** Check reversal of destructive or bulk changes.
- **Validation Timing:** Check inline versus late validation and preserved input after failure.

## 4. Repetition & Efficiency

- **Repetitive Input:** Find re-entering known data, missing defaults, and absent copy/duplicate features.
- **Bulk Actions:** Check multi-select and batch capabilities.
- **Keyboard Efficiency:** Check shortcuts, tab flow, and autofocus.
- **Form Fatigue:** Find long forms without chunking, saving, or autosave.
- **Navigation Cost:** Count steps for the most frequent tasks.

## 5. Recommendations

- **Impact Ranking:** Rank by error likelihood, severity, and frequency.
- **Concrete Redesigns:** Provide specific alternatives for the worst offenders.
- **Measurement:** Suggest metrics (time on task, error rate, abandonment) to validate improvements.

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
