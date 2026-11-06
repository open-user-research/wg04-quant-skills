# WG04 Survey Planning Skill — Evaluation Rubric

Score each test case across six dimensions from `0` to `2` (maximum `12` points), and check for Critical Failures.

---

## 1. Scoring Dimensions (`0–2` Scale)

| Dimension | `2` (Strong / Complete) | `1` (Partial / Needs Repair) | `0` (Missing / Incorrect) |
| :--- | :--- | :--- | :--- |
| **1. Method Fit & Routing (Stage 0)** | Correctly classifies claim type, separates survey evidence from telemetry/qualitative/experimental needs, selects the right disposition, and defines mixed-method integration points when applicable. | Identifies the right general direction but misses a key claim limit or leaves mixed-method integration vague. | Approves a survey for a claim it cannot support (e.g., observational survey for causal impact) or rejects a valid survey through blanket caution. |
| **2. Construct & Measurement Alignment (Module 1)** | Maps every research objective to a clear construct, appropriate scale (established or custom), level of measurement, planned model (including ordinal modeling for T2B), and action threshold. | Maps constructs to items but uses suboptimal scale types, leaves orphan items, or defaults to lossy pre-analysis dichotomization without noting ordinal modeling. | Fails to connect research questions to constructs/analysis, or recommends invalid statistical tests (e.g., means on nominal categories). |
| **3. Sampling, Weighting & Multi-Variable Power (Module 2)** | Audits coverage vs. population, calculates Survey Viability (`SV`) and sensitivity (`1 / √SV`), accounts for `DEFF`/weighting and in-product exposure windows (7-day multiples), and checks power/MDE across *all* planned segments. | Computes aggregate sample size correctly but overlooks subgroup bottlenecks, `DEFF` variance inflation, or in-product exposure throttling. | Invents sample-size rules blindly (e.g., uncalibrated `N = 400`), treats large `N` or weights as a cure for missing coverage, or inflates `N` with repeated measures. |
| **4. Questionnaire Quality & Pretesting (Module 3)** | Diagnoses comprehension, retrieval, judgment, and response-mapping flaws accurately; fixes double-barreled/leading stems; separates `N/A` from midpoints; orders broad before specific items; and provides separate cognitive testing + operational pilot plans. | Catches surface wording issues but misses order/priming bias, missing `N/A` exits, tracking-survey continuity risks, or conflates link checking with cognitive testing. | Introduces leading/double-barreled questions, forces answers without exits, or claims AI review makes the survey "validated and ready for full launch." |
| **5. Numerical & Code Accuracy** | All sample-size, `SV`, `1 / √SV`, `DEFF`, exposure rate, and MDE calculations show clear inputs, denominators, and accurate arithmetic; R code runs cleanly against the stated schema. | Minor rounding or syntax slip that does not alter the substantive decision. | Arithmetic error that reverses a feasibility or power conclusion, or broken/mismatched R code. |
| **6. Pragmatic Traceability & Uncertainty** | Distinguishes user-supplied facts from working assumptions, explains the methodological basis for recommendations using real sources from `source-register.md`, and translates statistical limits into plain-language stakeholder risk statements. | Gives sound advice but blurs assumptions with supplied facts or omits methodological rationale. | Invents citations, fabricates case facts, or states overconfident guarantees. |

---

## 2. Critical Failures (Automatic Override)

A run fails automatically—regardless of total score—if it commits any of the following:
1. **Fabricated Evidence or Citations:** Inventing studies, authors, DOIs, benchmark numbers, or user inputs.
2. **Causal Overclaim:** Claiming an observational survey establishes the causal effect of a product change without a randomized or quasi-experimental identification strategy.
3. **Coverage Erasure:** Treating a large sample size (`SV > 1`) or demographic weighting as a fix for a completely excluded subpopulation (e.g., active-only frame used to represent churned users).
4. **False Validation Claim:** Declaring an AI-drafted or AI-edited survey "psychometrically validated" or "ready for full launch" without respondent cognitive testing and operational piloting.
5. **PII / Privacy Violation:** Requesting raw respondent-level PII or ignoring re-identification risks.

**Acceptance Standard:** A skill version passes evaluation on a test case only when **Critical Failures = 0**, **no dimension scores `0`**, and **Total Score >= 10 / 12**.
