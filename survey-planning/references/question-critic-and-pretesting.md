# Module 3 · Survey Question Critic, Co-Creator & Pretesting

Use this module to improve an individual survey question (**Mode A**), critically audit an existing questionnaire (**Mode B**), draft a new questionnaire from a research brief (**Mode C**), and design a proportionate pretesting plan (**Cognitive Testing + Operational Piloting**).

---

## 1. Three Operating Modes & Their Scope

| Mode | Trigger / Input | Required Workflow & Output |
| :--- | :--- | :--- |
| **Mode A · Improve One Question** | One draft question (with or without context) | 1. Identify intended construct, audience, and reference timeframe.<br>2. Diagnose cognitive stage & wording/scale flaws.<br>3. If sound, say so. Otherwise return: (a) Original item, (b) Specific issue & effect on data, (c) Revised stem + matching response options, (d) Concise rationale, and (e) Warning if the edit shifts the construct or breaks longitudinal tracking comparability. |
| **Mode B · Review an Existing Survey** | Full or partial draft questionnaire | 1. Run Stage 0 Suitability check (do objectives fit a survey?).<br>2. Map objectives ↔ questions (flag unmeasured objectives & orphan items).<br>3. Audit item wording, scale architecture, skip logic, forced response, order/priming bias, and length/fatigue.<br>4. Classify issues as **`Critical`**, **`Major`**, or **`Minor`**.<br>5. Provide prioritized fixes, revised copy-ready items, and a pretesting plan. |
| **Mode C · Draft a New Survey** | Research brief, product problem, or Measurement Plan | 1. Confirm Stage 0 Suitability & Module 1 Measurement Map.<br>2. Select established UX measures or draft task-specific items + matching response options and skip logic.<br>3. Output copy-ready questionnaire (intro, screeners, core constructs, covariates, open-ends), Objective-to-Item-to-Analysis table, and pretesting plan. |

---

## 2. Theoretical Foundation: The 4-Stage Cognitive Response Model

Every survey item is a user interface task. Diagnose item flaws by checking where respondents will stumble across the four cognitive stages (Tourangeau, Rips, & Rasinski, 2000; Willis, 2005; Jarrett, 2021; Pearson, 2023):

| Cognitive Stage | What the Respondent Must Do | Common Design Failures to Flag |
| :--- | :--- | :--- |
| **1. Comprehension** | Interpret the question stem and response labels as intended | • **Internal product jargon / acronyms:** Using team terminology ("home feed surface", "workspace orchestration") that users do not share.<br>• **Double-barreled items:** Asking two things at once (*"How easy and useful was the export tool?"*).<br>• **Ambiguous concepts:** Abstract terms (*"trust"*, *"value"*, *"seamless"*) without behavioral or situational grounding.<br>• **Negatives / Double negatives:** Harder cognitive parsing and high error rates. |
| **2. Retrieval** | Search memory for the relevant episode or frequency | • **Unbounded or unrealistic recall windows:** Asking about minor UI interactions from "the past 6 months" or exact usage counts (*"How many times did you click filter last month?"*).<br>• **Reconstruction bias:** Respondents invent a plausible average rather than recalling actual episodes (Sauro & Lewis, 2024, Ch. 9). Anchor to a specific, recent episode (*"In your most recent session..."* or *"Over the past 7 days..."*). |
| **3. Judgment** | Summarize retrieved memories and form an evaluation | • **Leading / loaded stems:** *"How helpful was our new AI assistant?"* (presupposes helpfulness and nudges positive answers).<br>• **Hidden assumptions:** Asking all respondents to rate a feature some have never used.<br>• **High cognitive load:** Long forced-ranking lists (`> 5–6` items) where lower ranks degrade into random noise (Atsusaka & Kim; Pearson, *Anatomy of a survey question*).<br>• **Social desirability / acquiescence bias:** Agree/Disagree grids that invite passive agreement. |
| **4. Response Mapping** | Map the internal judgment onto the provided answer options | • **Stem-to-scale mismatch:** Asking *"How often..."* with an *Agree/Disagree* scale, or *"How easy or difficult..."* with an unbalanced unipolar scale.<br>• **Overlapping or non-exhaustive categories:** Age/tenure buckets like `1–3 years` and `3–5 years`, or missing common workflow alternatives.<br>• **Missing honest exits:** Forcing an answer without `Not applicable`, `Cannot recall`, or `Prefer not to answer`. |

---

## 3. Question Wording & Scale Architecture Rules

### A. Stem Wording & Reading Level
- **One question = one construct.** Split double-barreled stems or answer options immediately.
- **Keep language concrete and accessible:** Aim for a **6th- to 8th-grade reading level** for general consumer audiences (or appropriate domain terminology only when surveying verified technical/B2B specialists).
- **Prefer direct construct-specific scales over Agree/Disagree statements:** Instead of *"I found the checkout process easy to complete (Strongly Disagree – Strongly Agree)"*, ask directly: *"How easy or difficult was it to complete the checkout process? (Very difficult – Very easy)"*. Construct-specific scales reduce acquiescence bias and cognitive translation steps (Dillman, Smyth, & Christian, 2014; Saris et al., 2010).

### B. Rating Scales: Points, Balance, Labels & Midpoints
- **Bipolar vs. Unipolar matching:**
  - **Bipolar scales** have two opposite poles with a conceptual zero/neutral middle (e.g., *Very dissatisfied → Neither satisfied nor dissatisfied → Very satisfied*; *Very difficult → Neither → Very easy*). Use **5 or 7 points** and ensure the positive and negative sides are **strictly balanced** (2 negative, 1 neutral, 2 positive on a 5-point scale).
  - **Unipolar scales** measure zero to a maximum of one attribute (e.g., *Not at all useful → Slightly → Moderately → Very → Extremely useful*). Use **5 points**.
- **Fully label scale points:** Verbal labels on every point (rather than endpoint-only numerical scales, except in established instruments like `SEQ` or `0–10` LTR) improve reliability and clarify category meaning.
- **When to use a Binary (`Yes / No`) Question:** Do not force a 5-point Likert scale onto a judgment that is naturally binary for the user or decision (Pearson, *In defense of the yes or no question*). Binary questions are faster, reduce cognitive burden, translate cleanly across languages, and work well when measuring clear states or screening eligibility—provided you account for binary sample-size requirements.
- **Midpoints vs. Forced-Choice:** Include a substantive neutral midpoint (*Neither easy nor difficult*) when neutrality is a genuine attitude. Omit the midpoint (even-numbered scale) only when respondents have confirmed experience and the research goal specifically requires nudging leanings.

### C. `Not Applicable (N/A)`, `Don't Know`, and Forced Response Rules
- **Use skip logic first:** Route respondents past questions about features or experiences they have not had (Pearson, *Survey design: N/A and forced response*).
- **Keep non-substantive options distinct:** When skip logic cannot pre-filter every respondent, include explicit off-scale options (`Not applicable / Have not used`, `Cannot recall`, or `Prefer not to answer` for sensitive/demographic items) visually separated from the substantive rating scale. Never force someone who has no experience to pick the scale midpoint (`3`).
- **Avoid blanket forced-response rules:** Requiring every item to be answered increases survey abandonment and triggers frustrated random clicking or satisficing. Reserve mandatory responses for essential eligibility/routing screeners or core primary outcomes that include an honest `N/A` or `Prefer not to answer` exit.

### D. Question Ordering, Context Effects & Survey Fatigue
- **Funnel ordering & priming prevention (Tourangeau & Rasinski, 1988):**
  1. **Brief introduction:** Purpose, estimated time, confidentiality/privacy notice.
  2. **Essential screeners / routing items:** Only questions needed to determine eligibility or branch logic.
  3. **Broad / overall evaluations BEFORE specific diagnostic items:** Ask overall `CSAT` or overall ease *before* drilling into specific feature bugs; otherwise, recalling specific flaws primes respondents and artificially shifts the overall rating.
  4. **Core construct questions:** Place higher-effort items early while attention is high.
  5. **Open-ended diagnostic follow-up:** Use 1–2 targeted open-ended prompts (e.g., *"What was the main reason for your rating?"*) rather than many scattered text boxes.
  6. **Demographics / background / sensitive items:** Always place at the end (unless required up front for quota screening).
- **Randomize unordered lists:** Randomize option order in nominal multi-select/single-select lists (keeping `Other` and `None of the above` anchored at the bottom) to counter primacy and recency biases. Keep ordinal rating scales in consistent logical order.
- **Visual consistency (Couper, Conrad, & Tourangeau, 2007):** Maintain consistent scale direction (e.g., negative-to-positive left-to-right, or top-to-bottom on mobile) throughout the entire instrument. Avoid wide matrix grids that require horizontal scrolling on mobile devices.
- **Length & Channel Budgets:**
  - **In-product pop-up / intercept:** Maximum **1–5 questions** (`< 2–5 minutes`), minimal open-text.
  - **Email / uncompensated web survey:** Target **`< 7–10 minutes`**.
  - **Incentivized research survey:** Caution strongly against exceeding **15–20 minutes total**; align incentive value with actual completion time.

### E. Protecting Longitudinal / Tracking Surveys
Before editing any item in an existing survey, check whether it is part of a **recurring tracking study**. Even minor improvements to stem wording, scale labels, number of points, or preceding context questions can shift baseline distributions and break historical trend comparability (Bakhshi, 2026; WG04 Safeguard 4.1). If a tracking item is flawed, warn the researcher explicitly and recommend either preserving it for continuity or running a **split-ballot bridge calibration** (`50%` old wording, `50%` revised wording) for one wave.

---

## 4. Severity Classification for Survey Audits (Mode B)

When reviewing an existing questionnaire, group and prioritize findings using WG04's three-tier severity rubric:

| Severity | Definition | Concrete Examples |
| :--- | :--- | :--- |
| **`Critical`** | Fundamentally undermines the study's main objective, leads to invalid conclusions, or creates severe ethical/privacy risks. Must be resolved before proceeding. | • **Method mismatch:** Using stated intention to measure actual retention or causal impact.<br>• **Missing primary construct:** Research brief asks about checkout trust, but survey only asks about visual appearance.<br>• **Unnecessary PII / re-identification risk.** |
| **`Major`** | Substantially degrades accuracy, completeness, or interpretation of responses, though the overall study remains viable once fixed. | • **Leading stem:** *"How helpful was our support team?"*<br>• **Double-barreled item:** Asking about speed and accuracy in one rating.<br>• **Forced rating without N/A or skip logic** for a feature many users haven't tried.<br>• **Order priming:** Asking about outages right before overall satisfaction.<br>• **Unrealistic recall:** Asking for exact frequency 6 months ago. |
| **`Minor`** | Affects clarity, flow, or formatting polish without changing the underlying construct or conclusions. | • Slightly wordy phrasing that can be tightened.<br>• Inconsistent capitalization or redundant transition text. |

---

## 5. Pretesting Plan: Cognitive Testing + Operational Piloting

Never declare a survey ready for full launch based solely on an AI review. Always include a two-part respondent pretesting plan (Jarrett, 2021, Ch. 3 & Ch. 5; Sauro & Lewis, 2024, Ch. 18; Bergstrom et al., 2017; Pearson, 2023):

### Part 1 · Cognitive Survey Testing (Testing Respondent Interpretation)
**When it is essential:** Newly drafted custom questions, abstract constructs (e.g., AI trust, perceived value), complex trade-off tasks, multi-language translations, high-stakes product decisions, or new longitudinal tracking surveys (where errors propagate indefinitely).

- **Option A: Rapid Unmoderated Cognitive Test ("The Short Way" — adds ~1–2 days):**
  - Recruit **`4–5` participants** from the target audience (or `2–3` per major user segment across `2–4` segments) on an unmoderated testing platform (e.g., UserTesting, Userlytics) with the programmed survey link.
  - Instruct participants to think aloud while answering and focus on question clarity rather than just clicking through:
    - *Comprehension probe:* "In your own words, what is this question asking? Are there any terms (like `[term]`) that feel unclear or mean different things?"
    - *Retrieval/Judgment probe:* "How did you come up with your answer for the past `[time window]`? Was that easy or hard to remember?"
    - *Response-mapping probe:* "Did the answer choices include the option you wanted to pick? Was anything missing or overlapping?"
- **Option B: Moderated Cognitive Interviews ("The Long Way"):**
  - Use live moderated think-aloud + retrospective verbal probing (Willis, 2005; Bergstrom, 2017) when surveying hard-to-reach B2B/enterprise populations, sensitive topics, or high-stakes global instruments.

### Part 2 · Operational Pilot / Soft Launch (Testing the Collection & Analysis Pipeline)
A link check tests routing; cognitive testing tests interpretation; an **operational pilot** tests the end-to-end production system.
1. Field the survey to a small initial wave (e.g., **`30–50` completes** or `5–10%` of the invitation pool).
2. **Audit pilot telemetry & data capture:**
   - Check invitation delivery, click-to-complete dropout points, mobile vs. desktop rendering, and median completion time.
   - Check item nonresponse spikes, `% N/A` usage, and open-ended follow-ups (if open-ended answers talk about a different topic than the closed rating, the closed stem is being misread).
   - Inspect scale distributions for severe ceiling/floor effects or straightlining.
3. **Run the Module 1 Pre-Analysis R Script on the pilot export:** Verify that variable coding, skip-logic denominators, and weighting joins execute cleanly before releasing the remaining invitations.
