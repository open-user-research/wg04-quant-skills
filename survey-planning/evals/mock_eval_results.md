# WG04 Survey Planning Skill — Mock Evaluation Runs & Scored Results

This file records the full mocked outputs and rubric evaluation of the `survey-planning` v1.0.0 skill across the three test cases defined in [`cases.md`](cases.md).

---

## Summary Scorecard

| Test Case | WG04 Modules Exercised | 1. Method Fit | 2. Measurement | 3. Sampling & Power | 4. Question Quality | 5. Math & Code | 6. Traceability | Total Score | Critical Failures | Result |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Case 1 (C13):** Export Drop & Unknown Friction | Stage 0 + Module 3 | `2/2` | `2/2` | `2/2` | `2/2` | `N/A` | `2/2` | **10 / 10** (`12/12` eq.) | `0` | **PASS** |
| **Case 2 (C14 + C15):** AI Assistant Trust & Active-Only Frame | Stage 0 + Modules 1, 2, 3 | `2/2` | `2/2` | `2/2` | `2/2` | `2/2` | `2/2` | **12 / 12** | `0` | **PASS** |
| **Case 3:** Checkout Experiment, Ordinal T2B & Exposure Plan | Stage 0 + Modules 1, 2, 3 | `2/2` | `2/2` | `2/2` | `2/2` | `2/2` | `2/2` | **12 / 12** | `0` | **PASS** |

---

## Run 1 · Case 1 (Book-Grounded Case C13: Export Counts & Unknown Friction)

### Input Prompt
> "Our product telemetry shows how many active accounts completed a CSV export last month, and completion dropped 14%. Leadership wants us to launch a survey this week asking users why exporting feels difficult and which export bug hurt them most, though we haven't done qualitative research on the new export flow yet. Can you draft the survey?"

### Mocked Skill Output

#### 1. Stage 0 · Suitability & Method Routing Gate
- **Primary Disposition:** **`MIXED_METHOD`** (Exploratory Sequential Design: `Behavioral Telemetry + Qualitative/Usability Discovery → Optional Targeted Survey`)
- **Confidence:** **High**
- **Decisive Methodological Reason:** Your request bundles three distinct claims that require different evidence sources:
  1. **Magnitude of the export decline (`-14%`):** Already established by validated account telemetry. Do not ask users to self-report export frequency or completion counts in a survey—retrospective frequency recall suffers from reconstruction bias and cannot improve on complete event logs (*Sauro & Lewis, 2024, Ch. 1 & Ch. 9; Jarrett, 2021, Ch. 1*).
  2. **Discovering *why* exporting feels difficult when failure modes are unknown:** Because you have not yet observed the new export flow or identified the candidate friction categories, drafting a closed-ended "which export bug hurt you most?" checklist now will introduce **survey scope error** (missing the real usability trap and forcing respondents into guessed categories; *Pearson, 2026, Qual vs. Quant is more than Why vs. What*).
  3. **Causal attribution for the 14% drop:** Even if users report what frustrated them, a retrospective survey cannot isolate whether a recent code release, a data-size limit, or a seasonal workflow shift caused the 14% drop (*Bakhshi, 2026; Navarro, Ch. 2*).

#### 2. Recommended Mixed-Methods Route & Integration Point

| Step | Method | Research Question Resolved | Integration Point (Ladner, 2019) |
| :--- | :--- | :--- | :--- |
| **Step 1A (Immediate, Days 1–2)** | **Funnel Telemetry & Error-Log Breakdown** | Where in the export flow (click → modal → processing → download) does the 14% drop occur, and which browser/file-size segments are affected? | Isolates whether the drop is a technical failure (e.g., timeout on large files) or user abandonment in the UI. |
| **Step 1B (Immediate, Days 2–4)** | **Diagnostic Usability Observation (`n = 6–8`) + 2-Item In-Flow Intercept** | What unarticulated UI friction or error states do users encounter when attempting a CSV export? | Generates the grounded taxonomy of failure modes needed to either fix the bug directly or write valid closed-ended survey options. |
| **Step 2 (Conditional, Week 2)** | **Standardized Prevalence Survey** | Across the broader active account base, how prevalent is each discovered friction point by segment? | Only run Step 2 if Step 1 uncovers multiple competing workflow issues that require prevalence sizing to prioritize engineering effort. |

#### 3. Optional Immediate 2-Item In-Product Intercept (For Step 1B Discovery)
If you want to capture immediate in-context feedback from users right after they attempt (or abandon) a CSV export while Step 1A/1B runs, deploy this minimal 2-item intercept rather than a full email questionnaire:

1. **`Q1` [Perceived Task Ease — `SEQ`, 7-point bipolar]:**
   *"Overall, how easy or difficult was it to export your CSV today?"*
   - `1` = Very difficult · `2` = Difficult · `3` = Somewhat difficult · `4` = Neither easy nor difficult · `5` = Somewhat easy · `6` = Easy · `7` = Very easy
2. **`Q2` [Open-Ended Diagnostic Prompt — shown if `Q1 <= 4` or export abandoned]:**
   *"What, if anything, made exporting difficult or prevented you from finishing?"* `[Open text box — optional]`

- **Readiness Status:**
  - *Instrument Readiness:* Ready for immediate intercept deployment (uses standard `SEQ` + open-text discovery).
  - *Evidence Sufficiency:* **Supplementary evidence required** (pair with Step 1A export error logs and Step 1B usability observation).

---

## Run 2 · Case 2 (Combined Cases C14 & C15: Abstract Trust, Active-Only Frame & Subgroup Bottleneck)

### Input Prompt
> "We want to estimate how much all of our Q3 customers—including users who churned last month—trust our new AI coding assistant, and compare Free vs. Pro vs. Enterprise Admin segments. We'll email our currently active monthly users (`N_invite = 15,000`, expected usable completion yield `6%`) with a web survey asking: `'How much do you agree: I trust the AI assistant and find its suggestions accurate? (1 = Strongly Disagree to 5 = Strongly Agree, required)'`. We need `500` total responses and we'll just check that the survey link works before launching."

### Mocked Skill Output

#### 1. Stage 0 · Suitability & Method Routing Gate
- **Primary Disposition:** **`PLAN_WITH_CONDITIONS`** (Critical coverage, construct, subgroup sampling, and pretesting blockers must be resolved before launch)
- **Confidence:** **High**

| Dimension | Supplied Input / Assumption | Methodological Assessment | Consequence & Required Condition |
| :--- | :--- | :--- | :--- |
| **Coverage & Selection (`Critical Blocker`)** | Target population = *all Q3 customers including recent churners*; Frame = *currently active monthly users* (`15,000` emails) | **Zero coverage of churned users.** Churned customers are systematically more likely to have experienced low trust or poor accuracy. Achieving `900` responses from active users reduces sampling error (`SE`) but leaves coverage error untouched (*Sauro & Lewis, 2024, Ch. 2; Groves et al., 2009*). | **Condition 1:** Either add churned Q3 customers to the email invitation frame (and stratify/weight by retention status) OR explicitly narrow your research claim to *currently active Q3 customers*. |
| **Construct & Answerability (`Critical Blocker`)** | Draft item asks about `"trust"` and `"suggestions accurate"` together | `"Trust"` is an undefined, multi-dimensional construct (confidence in code correctness vs. data privacy/security vs. reliability), and the item is double-barreled (*Tourangeau et al., 2000; Sauro & Lewis, 2024, Ch. 6*). | **Condition 2:** Decompose "trust" into specific experiential dimensions and separate perceived accuracy from data/security trust. |
| **Subgroup Yield & Power (`Major Blocker`)** | Compare `Free` vs. `Pro` vs. `Enterprise Admin`; `N_invite = 15,000`, `6%` yield → `900` total completes | Aggregate Survey Viability is high (`SV = 900 / 500 = 1.80`), **but proportionate sampling starves the rare `Enterprise Admin` segment** (see Module 2 table below). | **Condition 3:** Oversample `Enterprise Admins` via disproportionate stratified sampling and apply design weights. |
| **Pretesting (`Major Blocker`)** | "We'll just check that the survey link works" | A link check only verifies URL routing. It does not test whether respondents interpret "trust" consistently (**Cognitive Testing**) or whether skip logic and data exports work (**Operational Pilot**) (*Jarrett, 2021, Ch. 3 & 5; Sauro & Lewis, 2024, Ch. 18*). | **Condition 4:** Run a rapid cognitive test (`4–6` users) on the new trust items plus a soft-launch operational pilot (`30–50` completes). |

---

#### 2. Module 2 · Sampling, Viability (`SV`), Weighting & Multi-Variable Power Audit

**Assumptions Labeled for Subgroup Audit:**
- Supplied: `N_invite = 15,000` active users, expected usable yield = `6%` (`n_actual = 900` total completes), aggregate target `n_planned = 500`.
- Working assumptions for segment shares in the active frame (adjust if your SQL counts differ): `Free = 65%`, `Pro = 32%`, `Enterprise Admin = 3%`, and anticipated post-stratification weighting Design Effect **`DEFF = 1.25`** (accounting for engagement/tenure nonresponse weights; *Valliant et al., 2018*).

**Aggregate Survey Viability:**
$$SV_{\text{aggregate}} = \frac{900}{500} = 1.80 \implies \text{Sensitivity Multiplier} = \frac{1}{\sqrt{1.80}} = 0.745\times$$
*(Aggregate MDE is ~25% smaller than planned—**for active users only**.)*

**Multi-Variable & Subgroup Power Audit (`α = .05` two-sided, `80%` Power, Baseline Top-2-Box `= 65%`):**

| Variable / Comparison | Segment / Stratum | Expected Raw `n` (`6%` yield) | Weighting `DEFF` | Effective Sample (`n_eff = n / DEFF`) | 95% CI Half-Width (`±MOE`) | Achievable `MDE` vs. `Pro` (Binary T2B) | Achievable `MDE` (Ordinal `clm` Model) | Risk Flag |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **Overall Active Estimate** | All Active (`100%`) | `900` | `1.25` | `720.0` | `±3.5%` | — | — | **Green** (for active users) |
| **Tier Comparison A** | `Free` (`65%`) vs. `Pro` (`32%`) | `585` vs. `288` | `1.25` | `468.0` vs. `230.4` | `±4.3%` / `±6.2%` | **`±10.8` pts** | **`±8.9` pts** | **Green / Amber** |
| **Tier Comparison B** | `Enterprise Admin` (`3%`) vs. `Pro` (`32%`) | **`27`** vs. `288` | `1.25` | **`21.6`** vs. `230.4` | **`±21.1%`** | **`±30.1` pts** | **`±24.8` pts** | **RED (Critically Underpowered)** |
| **Churned Q3 Segment** | `Churned Q3` (`0%` of frame) | **`0`** | — | **`0.0`** | Unestimable | Unestimable | Unestimable | **RED (Zero Coverage)** |

> **Plain-Language Stakeholder Risk Statement:**
> *"Emailing 15,000 active users at a 6% response rate will give us ~900 total responses—plenty to compare Free and Pro users (detecting a ~9–11 point difference). However, two fatal gaps remain: (1) Churned Q3 users are completely excluded, so we cannot make claims about all Q3 customers without adding churned users to the email pull, and (2) Enterprise Admins will yield only ~27 responses (`±21%` margin of error), meaning we would miss anything smaller than a 25–30 point gap. To fix this, we should invite all eligible Enterprise Admins and a stratified sample of Churned Q3 users, then apply design weights in R."*

---

#### 3. Module 3 · Mode A/B Critique of the Proposed Survey Item

- **Original Draft Item:**
  > *"How much do you agree: I trust the AI assistant and find its suggestions accurate? (1 = Strongly Disagree to 5 = Strongly Agree, required)"*

- **Diagnosed Flaws:**
  1. **Double-barreled stem (`Major` — Comprehension & Judgment):** Combines *overall trust* (which includes privacy/security and predictability) with *suggestion accuracy*. A user who finds code completions accurate (`4/5`) but worries about proprietary code leakage (`1/5`) cannot answer validly (*Gorvine et al., 2018*).
  2. **Forced response without eligibility routing or `N/A` (`Major` — Response Mapping):** Active account holders who have not used the AI coding assistant in the reference period are forced to fabricate an answer—usually inflating the `3 = Neither Agree nor Disagree` midpoint (*Pearson, Survey design: N/A and forced response*).
  3. **Agree/Disagree acquiescence bias & missing reference window (`Major` — Retrieval & Response Mapping):** Agree/Disagree statements increase acquiescence bias and require extra mental translation compared to direct construct-specific scales (*Dillman et al., 2014*).

- **Revised Copy-Ready Items (Splitting Eligibility, Perceived Accuracy, and Confidence/Trust):**

  - **`Q1` [Eligibility Screener & Usage Context — Single Select]:**
    *"In the past 14 days, have you used the AI coding assistant while writing or reviewing code?"*
    - `Yes` *(Continue to Q2–Q3)*
    - `No, I haven't used it in the past 14 days` *(Route to non-user barrier question)*
    - `I'm not sure what the AI coding assistant is` *(Route to end / awareness tally)*

  - **`Q2` [Construct 1: Perceived Suggestion Quality/Accuracy — 5-Point Bipolar Scale]:**
    *"Thinking about the code suggestions you received in the past 14 days, how would you rate their overall quality?"*
    - `1` = Very poor quality
    - `2` = Somewhat poor quality
    - `3` = Neither poor nor good quality
    - `4` = Somewhat good quality
    - `5` = Very good quality
    - *(Off-scale exit)* `Cannot recall`

  - **`Q3` [Construct 2: Confidence in Relying on Output ("Trust") — 5-Point Unipolar Scale]:**
    *"How confident do you feel merging code suggested by the AI assistant after your normal review?"*
    - `1` = Not at all confident
    - `2` = Slightly confident
    - `3` = Moderately confident
    - `4` = Very confident
    - `5` = Extremely confident
    - *(Off-scale exit)* `Not applicable — I never merge AI suggestions`

- **Two-Stage Pretesting Plan:**
  1. **Cognitive Testing (1–2 days):** Run an unmoderated think-aloud with `6` users (`2 Free`, `2 Pro`, `2 Enterprise Admins`) asking what *"confidence in merging"* and *"overall quality"* mean to them and whether any security/privacy trust concern is missing.
  2. **Operational Pilot (Soft Launch):** Send to `500` invitees (`~30` completes) first to verify `Q1` skip routing, check `% Cannot recall`, and test the post-stratification R script before sending the remaining invitations.

---

## Run 3 · Case 3 (End-to-End Plan: Checkout Experiment, Ordinal Top-2-Box & Exposure Plan)

### Input Prompt
> "We are running a randomized in-product A/B experiment (`Control` vs. `Simplified Checkout`) where users are randomly assigned at checkout. Beyond logged checkout conversion, we want an embedded post-checkout survey to test whether `Simplified Checkout` improves perceived checkout ease (action threshold: at least a `+6` percentage-point lift in Top-2-Box ease) and whether it reduces perceived payment confusion, broken out by `New` (`30%`) vs. `Returning` (`70%`) buyers. Daily eligible checkout traffic is `10,000` users per arm (`20,000` total), and we expect a `15%` view-to-complete rate on a 3-question intercept. Give us the full measurement plan, sampling/exposure & multi-variable power plan, questionnaire, and pre-analysis R code."

### Mocked Skill Output

#### 1. Stage 0 · Suitability & Method Routing Gate
- **Primary Disposition:** **`PLAN_SURVEY`** (Embedded Experimental Outcome Survey paired with A/B Telemetry)
- **Confidence:** **High**
- **Methodological Rationale:**
  - Because users are **randomly assigned** to `Control` vs. `Simplified Checkout`, comparing survey responses across arms supports a **causal inference** about the redesign's impact on perceived ease and confusion (*Bakhshi, 2026; Navarro, Ch. 2*).
  - **Key Experimental Safeguard:** Randomization occurs at checkout entry, whereas the survey captures *post-checkout respondents*. You must audit **differential nonresponse** (whether completion rates or buyer composition differ between `Control` and `Simplified Checkout` survey respondents) before claiming an unbiased treatment effect.
  - Keep actual checkout conversion, drop-off step, and time-to-complete in **production telemetry**; use the 3-item intercept strictly for perceived ease (`SEQ`), perceived payment clarity, and open-ended friction diagnosis.

---

#### 2. Module 1 · Measurement Map & Pre-Analysis Strategy

| Research Question | Hypothesis Type | Construct | Survey Item & Scale | Planned Statistical Model | Segments | Action Threshold / Decision Rule |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **RQ1 (Primary):** Does `Simplified Checkout` increase perceived checkout ease? | Confirmatory | Perceived task ease | `Q1` (5-point bipolar Ease scale: *Very difficult* to *Very easy*) | Cumulative logit ordinal model (`ordinal::clm`); derive Top-2-Box (`P(Y >= 4)`) lift & 95% CI via `emmeans` | Overall; `New` (`30%`) vs. `Returning` (`70%`) buyers | **Ship threshold:** Derived T2B ease lift `>= +6.0` percentage points (and lower 95% CI bound `> 0`) in both Overall and `New` buyers |
| **RQ2 (Secondary):** Does `Simplified Checkout` reduce perceived payment-step confusion? | Confirmatory | Perceived payment clarity | `Q2` (5-point bipolar Clarity scale: *Very confusing* to *Very clear* + `N/A`) | Cumulative logit (`ordinal::clm`) + derived Bottom-2-Box / Top-2-Box; BH-FDR adjustment for secondary family | Overall; `New` vs. `Returning` buyers | Reduction in perceived confusion (`OR >= 1.35`) |
| **RQ3 (Diagnostic):** What specific friction remains in the new checkout? | Exploratory | Self-reported friction reasons | `Q3` (Optional open-text shown when `Q1 <= 3` or `Q2 <= 3`) | Qualitative codeframe frequency by arm | `Control` vs. `Simplified` | Identify top residual usability defects before 100% rollout |

> **Why Ordinal Modeling (`ordinal::clm`) Beats Pre-Analysis Dichotomization Here:**
> Collapsing `Q1` into a `0/1` Top-2-Box indicator *before* running a two-proportion test discards all movement between scale points `1 → 3` and `4 → 5`. Fitting a proportional-odds cumulative logit model (`ordinal::clm`) to all 5 scale categories and **deriving the Top-2-Box probability from the model** delivers the exact same stakeholder percentage (`"76% vs. 70% Top-2-Box ease, +6 pts"`) while reducing the required sample size by **~35%** (*Pearson, 2026, Deriving Top-2-Box from Ordinal Models; Whitehead, 1993*).

---

#### 3. Module 2 · Multi-Variable Power Audit & 7-Day Exposure Plan

**Power & Sample Size Calculation (`α = .05` two-sided, `80%` Power, Baseline T2B `= 70%`, Target T2B `= 76%` [`+6` pts, `OR = 1.357`]):**
- **Naive Binary Two-Proportion Test (`70%` vs. `76%`):** Requires **`n = 856` per arm** (`1,712` total) for a single comparison.
- **Ordinal Cumulative Logit Model (`ordinal::clm`, baseline distribution `[5%, 10%, 15%, 40%, 30%]`):** Requires **`n = 559` per arm** (`1,118` total) for the same `+6` point T2B shift.
- **Powering the Bottleneck Subgroup (`New Buyers = 30%` of traffic):**
  To achieve `n = 559` *within* `New Buyers` per arm (`80%` power for the `+6` pt action threshold inside New Buyers using the ordinal model), total completes per arm must be:
  $$n_{\text{planned per arm}} = \frac{559}{0.30} = 1,864 \text{ completes per arm } (3,728 \text{ total})$$
  *(Note: Even if a user prefers the conservative binary test inside New Buyers, `856 / 0.30 = 2,854` per arm is easily achievable within your 7-day traffic—see exposure table below.)*

**Multi-Variable Power & Precision Table (at `n_planned = 1,864` per arm / `3,728` total, `DEFF = 1.00` unweighted randomized arms):**

| Variable / Test | Analysis Group | Sample per Arm (`n_1`, `n_2`) | Achievable `MDE` (Ordinal Derived T2B, 80% Power) | Achievable `MDE` (Naive Binary T2B, 80% Power) | 95% CI Half-Width per Arm (`±MOE`) | Status vs. `+6.0` pt Action Threshold |
| :--- | :--- | ---: | ---: | ---: | ---: | :--- |
| **`Q1: Checkout Ease (T2B)`** | **Aggregate (`All Buyers`)** | `1,864` vs. `1,864` | **`+3.3` pts** (`OR = 1.18`) | `+4.1` pts | `±2.1%` | **Green** (Well-powered below `+6` pt threshold) |
| **`Q1: Checkout Ease (T2B)`** | **`New Buyers` (`30%` share)** | **`559` vs. `559`** | **`+6.0` pts** (`OR = 1.36`) | `+7.4` pts | `±3.8%` | **Green** (Meets exact `+6.0` pt threshold via ordinal model) |
| **`Q1: Checkout Ease (T2B)`** | **`Returning Buyers` (`70%` share)** | `1,305` vs. `1,305` | **`+4.0` pts** (`OR = 1.22`) | `+4.9` pts | `±2.5%` | **Green** |
| **`Q2: Payment Clarity`** | **`New Buyers` (`30%` share)** | `559` vs. `559` | **`+6.0` pts** (`OR = 1.36`) | `+7.4` pts | `±3.8%` | **Green** |

**In-Product 7-Day Intercept Exposure & Throttling Plan:**
- **Daily eligible traffic:** `10,000` users/day per arm $\implies$ **`70,000` eligible users/week per arm** across a full 7-day weekday/weekend cycle.
- **Unthrottled weekly yield (`100%` exposure × `15%` completion):** `70,000 × 0.15 = 10,500` completes/arm/week (`SV = 10,500 / 1,864 = 5.63`).
- **Recommended Throttled Exposure Rate:** Set the intercept trigger to **`20%` random user-level exposure** across **7 full days**:
  $$n_{\text{actual per arm}} = 70,000 \times 0.20 \text{ (exposure)} \times 0.15 \text{ (yield)} = 2,100 \text{ completes per arm } (4,200 \text{ total})$$
  - **Resulting Survey Viability (`SV`):** `SV = 2,100 / 1,864 = 1.13` (`Sensitivity Multiplier = 1 / √1.13 = 0.94×`), providing a `13%` buffer for speeder/quality exclusions while avoiding over-surveying 80% of checkout users and capturing a balanced 7-day traffic mix.

---

#### 4. Module 3 · Copy-Ready 3-Item Post-Checkout Intercept Questionnaire

> **Intro Header:** *"Quick question about your checkout today (takes < 1 minute)"*

1. **`Q1` [Overall Perceived Checkout Ease — Placed FIRST before specific payment prompt to prevent priming]:**
   *"Overall, how easy or difficult was it to complete your checkout today?"*
   - `1` = Very difficult
   - `2` = Somewhat difficult
   - `3` = Neither easy nor difficult
   - `4` = Somewhat easy
   - `5` = Very easy

2. **`Q2` [Specific Construct: Perceived Payment Step Clarity]:**
   *"How clear or confusing were the payment options and billing details during checkout?"*
   - `1` = Very confusing
   - `2` = Somewhat confusing
   - `3` = Neither confusing nor clear
   - `4` = Somewhat clear
   - `5` = Very clear
   - *(Off-scale exit)* `Not applicable — I used a saved one-click payment`

3. **`Q3` [Conditional Diagnostic Open-End — Display via skip logic ONLY if `Q1 <= 3` OR `Q2 <= 3`]:**
   *"What was the main thing that felt difficult or confusing during checkout?"*
   - `[Open text field — optional]`

*(Note: `experiment_arm` [`Control` / `Simplified`] and `buyer_tenure` [`New` / `Returning`] are passed silently via survey metadata/embedded data rather than asking the user.)*

---

#### 5. Annotated Pre-Analysis R Script (Ordinal Model + Derived Top-2-Box + Nonresponse Check)

```r
# ==============================================================================
# WG04 Pre-Analysis Script: Simplified Checkout A/B Experiment Survey
# Primary Model: Cumulative Logit (ordinal::clm) -> Derived Top-2-Box via emmeans
# ==============================================================================
library(tidyverse)
library(ordinal)
library(emmeans)

# 1. Load Data & Check Differential Nonresponse Across Experiment Arms ---------
# invite_summary has columns: arm, invited_n, completed_n
invite_summary <- tibble(
  arm         = c("Control", "Simplified"),
  invited_n   = c(14000, 14000),
  completed_n = c(2085, 2115)
)
prop.test(invite_summary$completed_n, invite_summary$invited_n)

raw_df <- read_csv("checkout_intercept_responses.csv")

# 2. Apply Pre-Specified Quality Rules & Factor Coding -------------------------
ease_levels <- c(
  "Very difficult", "Somewhat difficult",
  "Neither easy nor difficult", "Somewhat easy", "Very easy"
)
clarity_levels <- c(
  "Very confusing", "Somewhat confusing",
  "Neither confusing nor clear", "Somewhat clear", "Very clear"
)

analytic_df <- raw_df %>%
  filter(duration_sec >= 5) %>% # Exclude sub-5-second bot/accidental clicks
  mutate(
    arm = factor(arm, levels = c("Control", "Simplified")),
    buyer_tenure = factor(buyer_tenure, levels = c("Returning", "New")),
    q1_ease = factor(q1_ease_raw, levels = ease_levels, ordered = TRUE),
    q2_clarity_clean = na_if(q2_clarity_raw, "Not applicable — I used a saved one-click payment"),
    q2_clarity = factor(q2_clarity_clean, levels = clarity_levels, ordered = TRUE)
  )

# 3. Primary Confirmatory Test (RQ1): Ordinal Model + Derived Top-2-Box --------
m_ease_overall <- clm(q1_ease ~ arm, data = analytic_df, link = "logit")
summary(m_ease_overall)

# Test proportional odds assumption (Brant / nominal likelihood-ratio test)
nominal_test(m_ease_overall)

# Derive Top-2-Box ("Somewhat easy" [4] + "Very easy" [5]) = 1 - P(Y <= 3)
# Cutpoint "Neither easy nor difficult|Somewhat easy" is threshold 3
emm_cum <- emmeans(m_ease_overall, ~ arm | cut, mode = "cum.prob")
emm_t2b <- contrast(
  regrid(emmeans(m_ease_overall, ~ arm | q1_ease, mode = "prob")),
  method = list("T2B_Prob" = c(0, 0, 0, 1, 1)),
  by = "arm"
)
print(emm_t2b)

# Estimate T2B percentage-point lift (Simplified - Control) with 95% CI
t2b_lift <- pairs(emm_t2b, reverse = TRUE) %>% confint()
print(t2b_lift)
# Decision rule: Ship if point estimate >= +0.06 (+6.0 pts) and lower.CL > 0

# 4. Subgroup Confirmatory Test (RQ1b): New vs. Returning Buyers ---------------
m_ease_sub <- clm(q1_ease ~ arm * buyer_tenure, data = analytic_df, link = "logit")
emm_sub_t2b <- contrast(
  regrid(emmeans(m_ease_sub, ~ arm | buyer_tenure * q1_ease, mode = "prob")),
  method = list("T2B_Prob" = c(0, 0, 0, 1, 1)),
  by = c("buyer_tenure", "arm")
)
pairs(emm_sub_t2b, by = "buyer_tenure", reverse = TRUE) %>% confint()
```
