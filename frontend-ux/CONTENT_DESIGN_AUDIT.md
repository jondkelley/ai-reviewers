# Comprehensive UX Writing, Terminology & Microcopy Audit

Act as a UX content strategist, technical writer, and localization-aware copy editor conducting an exhaustive, production-grade UX content and microcopy audit of this repository and everything it deploys, configures, or depends on.

Review all user-facing text in the interface and codebase, including labels, buttons, headings, tooltips, empty states, error messages, confirmation dialogs, emails, notifications, help text, and documentation.

Your objective is to identify **unclear or inconsistent terminology, jargon, unhelpful error messages, ambiguous calls to action, misleading confirmations, tone inconsistencies, and copy that hinders task completion or localization**.

Evaluate the system against mature, current industry standards (plain-language guidelines, content style guides, and inclusive language practice), emphasizing evidence over opinion.

Do not modify application code, run destructive or state-changing commands, or implement remediation yet.

Produce a comprehensive, prioritized Markdown assessment named `CONTENT_DESIGN_AUDIT.md` containing evidence-based findings and developer-ready recommendations.

---

## 1. Content Inventory

- **String Sources:** Locate hard-coded strings, i18n files, templates, and server-generated messages.
- **Content Types:** Catalogue UI labels, errors, emails, notifications, and help.
- **Voice & Tone:** Identify any existing style guide and whether copy follows it.

Document the observed implementation rather than assuming the intended design matches reality.

## 2. Terminology & Consistency

- **Concept Naming:** Find one concept called several names, or several concepts sharing a name.
- **Internal Jargon:** Find code-level or database terminology leaking into the UI.
- **Capitalization & Punctuation:** Check consistent style.
- **Action Labels:** Check verbs are specific ("Save changes") rather than vague ("Submit", "OK").
- **Abbreviations:** Check unexplained acronyms.

## 3. Messages & Guidance

- **Error Messages:** Check that errors say what happened, why, and what to do next, without blame or internals.
- **Validation Text:** Check specificity and tone.
- **Empty & Success States:** Check that they guide the next action.
- **Confirmation Dialogs:** Check that consequences are stated and button labels match the action.
- **Instructions & Help:** Check placement, brevity, and accuracy.
- **Notifications & Emails:** Check subject lines, clarity, and call to action.

## 4. Readability, Inclusion & Localization

- **Reading Level:** Check sentence length and complexity.
- **Inclusive Language:** Check biased, gendered, or idiomatic phrasing.
- **Localization Readiness:** Find concatenated strings, embedded markup, hard-coded plurals, date and number formats, and text expansion hazards.
- **Accessibility of Copy:** Check link text, alt text, and screen-reader clarity.

## 5. Recommendations

- **Rewrites:** Provide before/after examples for the highest-impact problems.
- **Glossary:** Propose a canonical terminology list.
- **Governance:** Recommend centralizing strings and review practice.

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
