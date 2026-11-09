# Comprehensive Usability, Discoverability & Behavioral Friction Audit

Act as a user research specialist, behavioral UX analyst, and usability evaluator conducting an exhaustive, production-grade usability and behavioral friction audit of this repository and everything it deploys, configures, or depends on.

Review the full interface and its flows, evaluated through heuristic analysis and cognitive walkthroughs of the code, templates, and interaction design.

Your objective is to identify **undiscoverable features, violated user expectations, confusing decisions, ambiguous controls, interaction friction, and moments where users are likely to hesitate, err, or abandon**.

Evaluate the system against mature, current industry standards (cognitive walkthrough, Nielsen heuristics, behavioral design principles, and mental-model alignment), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `USABILITY_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Method & Personas

- **Representative Users:** Define novice, occasional, and expert personas from the product's context.
- **Tasks:** Select realistic goals for each persona.
- **Evidence Limits:** State that findings are heuristic predictions to be validated with real users.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Discoverability

- **Affordances:** Check that interactive elements look interactive and static ones do not.
- **Hidden Features:** Find capabilities buried in menus, gestures, or hover states.
- **Labels & Icons:** Check that icons are understandable and labeled.
- **Onboarding Cues:** Check empty states, tooltips, and first-use guidance.
- **Search & Shortcuts:** Check findability for returning users.

## 3. Expectations & Mental Models

- **Convention Violations:** Find behavior that differs from platform or industry norms.
- **Predictability:** Check that outcomes of actions are clear before they are taken.
- **Terminology Match:** Check that wording matches user language.
- **Defaults:** Check that defaults are safe and sensible.
- **Surprising Side Effects:** Find actions with unexpected consequences.

## 4. Friction & Abandonment Risk

- **Cognitive Walkthrough:** At each step ask whether the user will know what to do, see the control, connect it to their goal, and understand the feedback.
- **Friction Points:** Find unnecessary steps, forced accounts, redundant confirmations, and slow feedback.
- **Error Experience:** Check recoverability and tone when things go wrong.
- **Trust & Reassurance:** Check cues around payment, deletion, and personal data.
- **Interruption Recovery:** Check resuming after leaving mid-task.

## 5. Findings & Validation

- **Severity Rating:** Rate by frequency, impact, and persistence.
- **Fix Recommendations:** Provide specific interaction changes.
- **Test Plan:** Propose usability tests, A/B tests, or analytics events to validate each major hypothesis.

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
