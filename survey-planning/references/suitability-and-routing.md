# Stage 0 · Survey Suitability & Method Routing Gate (Orchestrator)

Use this module when a researcher proposes a new survey, brings an unclear research brief, asks "should this be a survey?", or changes the target population, construct, recruitment route, or study design. Also run a rapid suitability check at the start of any full-survey review (Module 3, Mode B) or new-survey draft (Module 3, Mode C).

---

## 1. Establish the Minimum Context

Extract what is already supplied and separate **supplied facts**, **working assumptions**, and **unresolved unknowns** across seven intake elements:

1. **Decision or Learning Objective:**
   - What product, design, or strategy decision will this inform? Who will use the findings, by when, and what is the risk of being wrong (Minimum Viable Rigor)?
   - Distinguish **one-time insight/estimation** from **recurring longitudinal tracking** (where stability of wording, mode, and sampling frame is the methodology) and **causal evaluation**.
   - Allow legitimate discovery or baseline monitoring goals without inventing a fake numeric action threshold.
2. **Research Questions & Intended Claim:**
   - Classify the claim: (a) discovering unknown friction/categories, (b) estimating prevalence or magnitude, (c) comparing segments, (d) understanding reported reasons/perceptions, (e) predicting future behavior, or (f) estimating the causal effect of a change.
   - Sketch a provisional **Goal → Evidence Needed → Measure → Planned Analysis** connection.
3. **Construct & Target Population:**
   - Define the construct, relevant experience, and reference time window.
   - Specify the unit of inference: individual people, accounts, organizations, user sessions, or repeated observations. Keep respondent counts distinct from repeated-observation counts.
4. **Existing Evidence:**
   - Check what product telemetry/logs, support records, usability tests, interviews, or prior surveys already establish—and where logs are incomplete or unvalidated.
5. **Recruitment Route & Reach:**
   - Identify the sampling frame, contactable eligible pool, exclusions/cooldowns, **invitation channel** (e.g., email, in-product prompt, SMS), and **completion mode** (e.g., web questionnaire, embedded micro-survey).
6. **Practical Constraints:**
   - Timeline, incentive budget, respondent burden limits, localization/accessibility needs, privacy/regulatory rules, and the team's analysis capability (e.g., comfort with R, weighting, or specialized methods like MaxDiff/conjoint).
7. **Precision or Effect Requirements:**
   - Smallest decision-relevant effect size or confidence interval width, if known (hand off detailed calculations to Module 2).

> **Intake discipline:** If the decision, claim, or target population is missing and could reverse the recommendation, ask 1–3 focused questions before recommending a survey. If the method mismatch is already clear, explain it right away without forcing an irrelevant intake.

---

## 2. Evaluate Six Methodological Dimensions Independently

Evaluate each dimension on its own merits. A high score or large sample on one dimension cannot compensate for a fatal flaw on another (Groves et al., 2009; Sauro & Lewis, 2024, Ch. 2).

### Dimension 1 · Construct & Answerability (Measurement Error)
- **Is the concept clearly defined?** Distinguish perceived ease, usefulness, satisfaction, trust, stated intention, recalled behavior, and observed task performance.
- **Can respondents answer accurately?** Check the four cognitive response stages (Tourangeau, Rips, & Rasinski, 2000; Jarrett, 2021, Ch. 3):
  1. *Comprehension:* Do respondents understand the terms and scope without internal product jargon?
  2. *Retrieval:* Can they recall the experience within the requested time window without severe memory distortion or reconstruction bias (Sauro & Lewis, 2024, Ch. 9)?
  3. *Judgment:* Does the item demand difficult mental arithmetic, trigger social desirability bias, or bundle multiple ideas?
  4. *Response mapping:* Do the response categories match the question and include honest exits (`Not applicable`, `Cannot recall`)?
- **Are response categories known?** If the team does not yet know the plausible reasons or categories to put in closed-ended options, conduct qualitative discovery or open-ended piloting before running a standardized prevalence survey.

### Dimension 2 · Inference & Study Design (Internal Validity)
- **Observational vs. Causal Claims:** An observational survey describes distributions and associations. It cannot isolate whether a product redesign caused a metric drop—even if you ask respondents *why* they did something (Pearson, 2026, *Qual vs. Quant is more than Why vs. What*; Bakhshi, 2026).
- **Surveys Inside Experiments:** A survey *can* support a causal claim when used as the outcome measure inside a randomized experiment (e.g., A/B test or factorial vignette survey) or a justified quasi-experimental design—provided you check for differential nonresponse across conditions.
- **Leading vs. Lagging Claims:** Most UX surveys (SUS, SEQ, PSSUQ, CSAT) are lagging summaries of prior experience. Do not treat a survey score as a proxy or leading indicator for future retention or adoption unless it is validated prospectively against future telemetry beyond prior behavior (Pearson, 2026, *Literature Review on Survey Behavior Indicators*).

### Dimension 3 · Coverage & Selection (Coverage & Nonresponse Error)
- **Population vs. Reachable Frame:** Who is in the target population, and who is excluded by the sampling frame or invitation channel?
  - *Classic trap:* Surveying only currently active users (via in-app intercept or active-user email list) when the research question includes churned users, abandoners, or non-users.
- **Nonresponse Bias:** Engaged, satisfied, or power users respond at higher rates than disengaged or frustrated users. Large `N`, demographic quotas, or opt-in panels do not eliminate nonresponse bias (Trochim; Sauro & Lewis, 2024, Ch. 2).
- **Limits of Weighting:** Post-stratification or raking weights can adjust for unequal selection and nonresponse on *measured* population variables (e.g., tenure, engagement tier, country), provided every stratum has respondents. Weighting **cannot** recover a subpopulation that had zero probability of being surveyed (e.g., uncontacted churners).

### Dimension 4 · Feasibility & Recruitment Yield (Sampling Error)
- **Check Survey Viability (`SV`) early:** Compare expected usable completes against the planned analytic sample requirement (`SV = expected_completes / required_completes`).
- **Account for subgroup bottlenecks:** A study with 600 total responses may still fail if a critical decision segment only yields 18 responses.
- **Small bounded populations:** If the entire population is small (e.g., 25 enterprise client accounts) and the goal is a bounded census description with follow-up calls rather than generalizing to a broader market, a short survey or structured intake is viable—focus on coverage and informant selection rather than an arbitrary minimum `N = 400` cutoff.

### Dimension 5 · Method Complexity & Team Readiness
- **Match method complexity to analytical support:** Do not recommend specialized methods (conjoint, discrete choice experiments, MaxDiff, latent class segmentation, multilevel ordinal models) unless the decision requires that structure and the researcher has the tooling and time to analyze and communicate it (WG04 Orchestrator guidelines).

### Dimension 6 · Alternatives & Mixed-Methods Integration
- Compare a survey against the strongest alternative or sequence of methods:

| If the Research Goal Is... | Primary Method Route | Role of a Survey (if any) |
| :--- | :--- | :--- |
| **Actual feature usage, frequency, conversion, or retention counts** | **Product Telemetry / Event Logs** (or support/transaction records) | None for the count itself; use a survey only if logs are missing/untrusted (with explicit recall limits) or to pair attitudes with logged behavior. |
| **Observed task success, time-on-task, or interface usability traps** | **Formative Usability Testing** or **Quantitative Usability Benchmarking** | Pair tasks with post-task ease (`SEQ`) and post-test perceived usability (`SUS` / `UX-Lite`). |
| **Discovering unknown pain points, mental models, or why users abandon** | **Qualitative Interviews, Field Studies, or Usability Observation** | Run qualitative discovery *first* to generate valid categories, then follow with a survey if prevalence estimation is needed (**exploratory sequential design**). |
| **Estimating prevalence, magnitude, or segment differences in attitudes/perceptions** | **Quantitative Survey** | Primary method, subject to construct, coverage, and sample viability checks. |
| **Testing whether a product change caused a shift in user sentiment or behavior** | **Controlled Experiment (A/B test, switchback, or factorial vignette)** | Use the survey as the randomized outcome measure or to diagnose experiential mechanisms alongside behavioral metrics. |
| **Forecasting future demand, adoption, or willingness to pay** | **Behavioral Fake-Door / Smoke Tests, Pilots, or Historical Holdout Models** | Treat stated intention as a bounded upper-bound or relative ranking signal (e.g., MaxDiff), never as a direct adoption or sales forecast. |

When recommending **Mixed Methods**, specify:
1. **Sequence:** Sequential exploratory (`Qual → Quant`), sequential explanatory (`Quant → Qual`), or concurrent (`Qual + Quant`).
2. **Division of labor:** Which exact question each method answers.
3. **Integration point:** How findings from Method 1 change the design of Method 2, or how the two datasets merge in the final decision (Ladner, 2019).

---

## 3. Dispositions & Handoff Output Structure

Select one primary disposition for the proposed survey (and route individual research questions separately if they differ):

1. **`PLAN_SURVEY` (Proceed with survey planning):** The survey fits the intended claim and no critical blocker exists. Move to Modules 1–3.
2. **`PLAN_WITH_CONDITIONS` (Proceed only after resolving stated conditions):** Survey fit is defensible, but a critical coverage, construct, sample viability, or causal-design condition must be resolved before launch.
3. **`MIXED_METHOD` (Use a survey as one component):** Separate the survey-appropriate objectives from objectives requiring telemetry, usability observation, or qualitative discovery, and define the integration point.
4. **`OTHER_APPROACH` (Use another method instead):** A survey cannot establish the needed evidence. Recommend the best alternative without quietly changing the user's research question to force a survey.
5. **`CLARIFY` (Clarify before routing):** Missing context could reverse the method recommendation. Ask 1–3 decisive questions and provide a conditional route.

### Recommended Stage 0 Output Template

- **Disposition & Confidence:** Primary disposition (`PLAN_SURVEY`, `PLAN_WITH_CONDITIONS`, `MIXED_METHOD`, `OTHER_APPROACH`, or `CLARIFY`), confidence level (`High` / `Moderate` / `Low`), and the decisive methodological reason.
- **Refined Research Brief:**
  - *Decision & Action Threshold:* What action depends on the results.
  - *Target Population, Unit & Time Window:* Who and what experience are in scope.
  - *Question-by-Question Route:* Table mapping each research question to its claim type, best evidence source/method, and claim limits.
- **Risk & Error Audit:** Summary of **Critical Blockers** vs. **Manageable Risks** across Construct/Answerability, Inference, Coverage/Nonresponse, and Feasibility/Yield.
- **Next Module Handoff:**
  - *To Module 1 (Measurement & Pre-Analysis):* Constructs to operationalize, candidate scales, and required segment comparisons.
  - *To Module 2 (Sampling & Power):* Population frame, invitation pool, expected yield, weighting variables, and subgroup targets.
  - *To Module 3 (Question Critic & Pretesting):* Draft items, channel/length constraints, cognitive testing flags, and pilot requirements.
