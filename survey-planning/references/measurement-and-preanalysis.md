# Module 1 · Measurement Strategy & Pre-Analysis Plan

Use this module to connect research goals to measurable constructs and survey items (**Measurement Plan** for stakeholders) and to specify variable construction, data quality rules, statistical tests, and annotated R code before fielding (**Pre-Analysis Plan** for the research team).

Writing the analysis plan *while* the survey is being designed prevents orphan items, unmeasured research questions, scale-to-method mismatches, and post-hoc p-hacking.

---

## 1. Entry Points & Workflow

Researchers may enter this module at any stage:
1. **Goals only (no survey yet):** Build the Measurement Map and Pre-Analysis Plan from scratch, then pass construct specifications to Module 3 to draft items.
2. **Existing survey draft + goals:** Audit coverage, flag gaps (unanswered research questions or orphan items with no purpose), verify that scales support the intended analyses, and produce the Pre-Analysis Plan.
3. **Stakeholder questions / feedback:** Map stakeholder requests onto existing items and produce a gap report showing what the instrument can and cannot answer.
4. **Finalized Measurement Plan:** Generate the concrete Pre-Analysis Plan, dummy tables/chart shells, and annotated R script.

---

## 2. Building the Measurement Plan (`Goals → Words`)

### Step 1 · Decompose Research Questions into Constructs
- Break broad goals ("Do users like the new checkout?") into specific, single-concept constructs:
  - **Pragmatic / Task-Focused Constructs:** Perceived ease of use, perceived usefulness/utility, task completion confidence, customer effort, perceived workload, information clarity.
  - **Hedonic / Relationship Constructs:** Overall satisfaction (CSAT), trust, perceived value/price-value, enjoyment/engagement, brand/product attitude.
  - **Behavioral / Intention Constructs:** Continuance intention, likelihood to recommend (NPS/LTR), self-reported workflow context (only when unlogged).
- Separate **confirmatory** hypotheses (pre-specified directional tests tied to a product decision) from **exploratory** questions (descriptive profiling or hypothesis generation).

### Step 2 · Select Established UX Scales vs. Custom Items
Prefer established, psychometrically evaluated scales when they match the construct, target audience, and reference experience. Never assume an adapted or shortened item retains its original psychometric properties without testing.

#### Standardized UX & CX Measures Reference & Behavioral Evidence Map

| Measure / Scale | Items & Format | Best Use Case | Behavioral Evidence & Limitations (Pearson, 2026; Sauro & Lewis, 2024) |
| :--- | :--- | :--- | :--- |
| **`SEQ` (Single Ease Question)** | 1 item, 7-point (*Very Difficult* to *Very Easy*) | Immediately post-task in usability studies or task-specific in-product flows | **Grade C (Lagging, task-local):** Correlates moderately with task completion (`r = .51`), time (`r = -.47`), and errors (`r = -.44`). Stronger link to task behavior than global scales. |
| **`UX-Lite` / `UMUX-Lite`** | 2 items, 5- or 7-point agreement (*Easy to use* + *Features meet my needs* / *Useful*) | Concise retrospective product/feature usability + usefulness pulse | **Grade C:** High convergence with `SUS`; separates pragmatic ease from usefulness (TAM alignment). Pair with telemetry for actual adoption. |
| **`SUS` (System Usability Scale)** | 10 items (alternating positive/negative), 5-point agreement (0–100 score) | Global perceived usability benchmarking across systems or releases | **Grade C (Lagging, global):** Extensive industry benchmarks (mean ~68). Small person-level correlation with task time/completion (`r ~ .16–.20`); do not use as a substitute for observed task success. |
| **`PSSUQ` / `CSUQ`** | 16 or 19 items, 7-point agreement + `N/A` | Detailed post-study (`PSSUQ`) or field (`CSUQ`) usability diagnosis (System Usefulness, Info Quality, Interface Quality) | **Grade C/D:** Useful when sub-dimensions (information vs. interface quality) matter. |
| **`SUPR-Q`** | 8 items (Usability, Trust, Appearance, Loyalty) | Website experience benchmarking | **Grade D:** Strong psychometrics; keep future-oriented loyalty items separate when modeling behavior. |
| **`NASA-TLX`** | 6 dimensions (Mental, Physical, Temporal, Performance, Effort, Frustration) | Diagnosing perceived cognitive/task workload in complex workflows | **Grade C:** Sensitive to workload manipulations; can dissociate from raw task speed when users compensate with higher effort. |
| **`CSAT` (Cumulative or Episode Satisfaction)** | 1 item, 5- or 7-point bipolar (*Very Dissatisfied* to *Very Satisfied*) | Relationship health or post-interaction appraisal | **Grade A (Dual indicator):** Summarizes prior experience and shows modest prospective prediction of retention (`r = .21` with actual retention behavior vs. `.60` with stated intention; Mittal et al., 2023). |
| **`NPS` / Likelihood to Recommend** | 1 item, 0–10 scale (often collapsed into Promoters − Detractors) | Executive communication metric when mandated by organization | **Grade B (Caution):** Throwing away information via 3-bucket categorization reduces precision. Independent studies show Top-2-Box `CSAT` performs as well or better (de Haan et al., 2015). If required, **analyze the raw 0–10 or ordinal distribution**, not just the collapsed Net Promoter score. |
| **Customer Effort Score (`CES`)** | 1 item, 5- or 7-point ease/effort | Post-support or service-resolution friction diagnostic | **Grade C:** Strong episode diagnostic; weak independent evidence as a standalone retention predictor. |
| **Behavioral / Continuance Intention** | 1–3 items, 5- or 7-point likelihood/probability | Early voluntary adoption risk-ranking | **Grade B:** Correlates `r ~ .35` (~12% shared variance) with future logged use; prior logged behavior dominates intention once habits form (Venkatesh et al., 2002; Wu & Du, 2012). |
| **PMF "Very Disappointed" Item** | 1 item, 4-point (*Very disappointed*, *Somewhat*, *Not disappointed*, *N/A*) | Exploratory product-market-fit segmentation | **Grade D:** The "40% Very Disappointed" threshold has no peer-reviewed prospective validation against retention or growth. Use descriptively, not as a hard gate. |

### Step 3 · Produce the Measurement Map & Gap Report
Every retained question must carry an explicit role: **Primary Construct**, **Covariate/Moderator**, **Screener/Routing**, **Weighting Benchmark**, or **Data Quality Check**.

| Research Question / Objective | Hypothesis Type (`Confirmatory` / `Exploratory`) | Construct | Survey Item(s) & Scale Type (`Nominal`, `Ordinal`, `Continuous`) | Planned Analysis & Summary Metric | Segments / Comparisons | Action Threshold / Decision Rule |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *RQ1: Does the redesigned editor reduce perceived formatting difficulty?* | Confirmatory | Perceived task ease | `Q3` (7-pt ordinal `SEQ`: *Very difficult* to *Very easy*) | Ordinal logistic regression (`ordinal::clm`); derived Top-2-Box (`>= 6`) lift + 95% CI | New vs. Legacy editor arms; Power vs. Casual users | Ship redesign if T2B ease increases by `>= 8` percentage points (or lower 95% CI bound `> +2` pts) |

**Gap Report Checklist:**
- **Unanswered Research Questions:** Objectives in the brief that have no corresponding survey item or behavioral data source.
- **Orphan Items ("Purpose Creep"):** Draft questions that do not map to any research objective, routing rule, or weighting variable—recommend cutting them to reduce fatigue.
- **Scale-to-Analysis Mismatches:** E.g., computing means/t-tests on unordered nominal categories, or relying on a single binary item when fine-grained sensitivity is required.

---

## 3. Building the Pre-Analysis Plan (`Words → Numbers`)

Specify all analytical choices *before* data collection begins:

### A. Data Quality & Exclusion Rules (Pre-Fielding Specification)
Define objective, auditable criteria for removing low-quality responses (Meade & Craig, 2012; Sauro & Lewis, 2024):
1. **Speeders:** Flag respondents completing in less than `1/3` to `1/2` of the median pilot completion time (or below a minimum reading-speed threshold, e.g., `< 2` seconds per closed item).
2. **Straightliners (Longstring):** Flag respondents who select the identical scale point across a grid or consecutive block of `>= 8` items (especially when reverse-worded or conceptually distinct items are included).
3. **Consistency / Attention Checks:** Prefer bogus/instructed-response items or semantic synonym/antonym consistency pairs only in long surveys (`> 10–15` min); never fail a respondent on a single ambiguous trap question.
4. **Multivariate Outliers (Multi-item scales):** Use Mahalanobis distance (`D^2`) on multi-item psychometric blocks when appropriate.
5. **Open-Text Gibberish / Bot Screen:** Screen open-ended responses for copy-pasted text, duplicated strings across respondents, or off-topic spam.
- *Rule:* Report both the raw `N` and cleaned analytic `N`, and run a sensitivity check if exclusions exceed `10–15%` of completes.

### B. Missing Data, `Not Applicable`, and `Don't Know` Handling
- **Separate substantive responses from non-substantive exits:** `Not applicable (N/A)`, `Cannot recall`, and `Prefer not to answer` must be coded as explicit missing/exit categories (`NA` with reason codes in R), **never** merged into the scale midpoint (`3 = Neither agree nor disagree`) or coded as `0`.
- **Specify the denominator for every percentage:** State whether percentages are calculated out of *all respondents*, *all eligible respondents shown the item via skip logic*, or *all respondents providing a substantive rating (excluding N/A)*. Also report the `% N/A` separately when it is informative (e.g., 35% of respondents had not used the feature).

### C. Variable Construction & The Ordinal Top-2-Box Framework
Stakeholders love Top-2-Box (`T2B`, e.g., `% Somewhat + Very Satisfied`) because a percentage is immediately interpretable. However, **dichotomizing a 5- or 7-point ordinal scale into `0/1` *before* analysis throws away distribution shifts (e.g., moving users from `1` to `3` or `4` to `5`), reduces statistical power, and inflates required sample size.**

**The WG04 Best-Practice Standard (Pearson, *Deriving Top-2-Box from Ordinal Models*):**
1. **Model the full ordinal scale** using a cumulative link model:
   $$\text{logit}(P(Y \le k)) = \theta_k - \eta$$
2. **Derive Top-2-Box (`P(Y >= K - 1)`) from the fitted model** as a post-estimation marginal probability:
   - **Path 1 (Frequentist, Proportional Odds assumed):** Fit `ordinal::clm(y ~ group, data = df)` and extract group-level category probabilities and delta-method confidence intervals via `emmeans::emmeans(m, ~ group, mode = "prob")`.
   - **Path 2 (Frequentist, Proportional Odds violated):** Relax parallel slopes via `ordinal::clm(y ~ group, nominal = ~ group)` or `VGAM::vglm(..., cumulative(parallel = FALSE))` when Brant / nominal likelihood-ratio tests show the treatment shifts only one tail of the scale.
   - **Path 3 / Path 4 (Bayesian cumulative logit, PO or non-PO):** Fit `brms::brm(y ~ group, family = cumulative("logit"))` (or `y ~ cs(group)` for threshold-varying effects), draw posterior category probabilities with `tidybayes::add_epred_draws()`, and sum the top two categories per `.draw`. This yields exact credible intervals on T2B lift and stakeholder-friendly posterior probability statements (e.g., *"94% probability that Design B exceeds Design A on Top-2-Box ease"*).

### D. Matching Statistical Models to Question Types

| Outcome Type | Unweighted Analysis Method | Weighted Survey Analysis (`survey` / `srvyr`) | Effect Size & Uncertainty to Report |
| :--- | :--- | :--- | :--- |
| **Single Binary Item (`Yes/No`, Task Success)** | Adjusted-Wald (Agresti-Coull) or Wilson 95% CI; logistic regression (`glm`) or 2-sample proportion test | `svyciprop(..., method = "logit")`; `svyglm(..., family = quasibinomial())` | Percentage point difference (`RD`), Risk Ratio (`RR`) or Odds Ratio (`OR`), + 95% CI |
| **Single Ordinal Likert Item (`5-pt` / `7-pt`)** | Cumulative logit (`ordinal::clm`) + derived T2B via `emmeans` (or Mann-Whitney / Wilcoxon + Hodges-Lehmann shift) | `survey::svyolr()` or weighted `svyglm` / design-adjusted ordinal model | Derived T2B % per group, T2B percentage-point lift + 95% CI, and cumulative Odds Ratio (`OR`) |
| **Multi-Item Validated Scale (`SUS`, `PSSUQ`)** | Check internal consistency (`psych::alpha` / `omega`); Welch's t-test, linear regression (`lm`), or mixed model (`lme4::lmer` for repeated measures) | `survey::svymean()`, `survey::svyttest()`, `survey::svyglm()` | Raw point difference (e.g., `+6.5 SUS points`), standardized effect (`Cohen's d` / `Hedges' g`), + 95% CI |
| **Multi-Select ("Select all that apply")** | Analyze each option as a separate binary indicator; use McNemar's test or mixed-effects logistic regression for within-respondent option comparisons | `svyciprop()` per option; Rao-Scott adjusted $\chi^2$ (`svychisq`) | Option selection % + 95% CI (note that percentages sum to `> 100%`) |
| **Ranking / MaxDiff** | Multinomial logit / hierarchical Bayes (`support.BWS`, `mlogit`, `brms`) or Plackett-Luce model (avoid raw means on long forced ranks due to random noise in lower ranks) | Weighted share of preference | Preference share (%) or rescaled 0–100 utility score + 95% CI |

### E. Multiple Comparisons & Action Thresholds
- **Control false discoveries:** When testing a family of exploratory segment comparisons or multiple items without a single primary outcome, apply **Benjamini-Hochberg False Discovery Rate (`p.adjust(p, method = "BH")`)** for discovery/diagnostic families or **Holm-Bonferroni (`method = "holm"`)** for strict familywise error control.
- **Action Thresholds over bare `p < .05`:** Pair every confirmatory test with a practical **Action Threshold** (Minimum Effect of Practical Interest). Distinguish four outcomes using the 95% CI:
  1. *Clear practical win:* Entire 95% CI lies above the action threshold (or above `0` with point estimate exceeding threshold).
  2. *Statistically detectable but practically trivial:* 95% CI excludes `0` but lies below the action threshold.
  3. *Inconclusive / underpowered:* 95% CI spans both `0` and the action threshold.
  4. *Clear null / equivalence:* 95% CI lies entirely below the action threshold (TOST equivalence logic).

---

## 4. Annotated Pre-Analysis R Script Template

Include an executable, self-contained R template matched to the planned schema whenever producing a Pre-Analysis Plan:

```r
# ==============================================================================
# WG04 Pre-Analysis Script Template
# Study: [Study Name] | Pre-Specified Date: [YYYY-MM-DD]
# ==============================================================================
library(tidyverse)
library(ordinal)
library(emmeans)
library(survey)
library(srvyr)

# 1. Load Data & Apply Pre-Specified Exclusion Rules ---------------------------
raw_df <- read_csv("survey_responses.csv")

 median_time <- median(raw_df$duration_sec, na.rm = TRUE)
analytic_df <- raw_df %>%
  filter(
    consent == "Yes",
    duration_sec >= (median_time / 3), # Speeder screen (< 1/3 median time)
    !is_straightliner                  # Pre-computed longstring screen on grid
  ) %>%
  mutate(
    # Separate N/A and Don't Know from substantive ordinal scale (1 to 5)
    q_ease_clean = na_if(q_ease_raw, "Not applicable"),
    q_ease_clean = na_if(q_ease_clean, "Cannot recall"),
    q_ease_ord   = factor(
      q_ease_clean,
      levels = c("Very difficult", "Somewhat difficult", "Neither",
                 "Somewhat easy", "Very easy"),
      ordered = TRUE
    ),
    segment = factor(segment, levels = c("Control", "Treatment"))
  )

cat("Raw N:", nrow(raw_df), "| Analytic N:", nrow(analytic_df), "\n")

# 2. Hypothesis H1: Ordinal Model + Derived Top-2-Box (Unweighted) -------------
# Model full 5-point ordinal distribution via cumulative logit
m_h1 <- clm(q_ease_ord ~ segment, data = analytic_df, link = "logit")
summary(m_h1)

# Check proportional odds assumption (nominal test)
nominal_test(m_h1)

# Derive Top-2-Box ("Somewhat easy" + "Very easy") probabilities & CIs
# P(Y >= 4) = 1 - P(Y <= 3); cutpoint 3 is "Neither|Somewhat easy"
emm_probs <- emmeans(m_h1, ~ segment | q_ease_ord, mode = "prob")
print(emm_probs)

# 3. Survey Weighting & Design-Adjusted Estimation (When Applicable) -----------
# Post-stratification / Raking using population benchmark totals
# pop_targets <- tibble(tenure_tier = c("New", "Established"), Freq = c(30000, 70000))
# svy_design <- analytic_df %>%
#   as_survey_design(ids = 1) %>%
#   postStratify(strata = ~tenure_tier, population = pop_targets)
#
# # Calculate Kish's Design Effect (DEFF) and effective sample size
# w <- weights(svy_design)
# deff_kish <- 1 + (sd(w) / mean(w))^2
# n_eff <- nrow(analytic_df) / deff_kish
# cat("Kish DEFF:", round(deff_kish, 2), "| Effective N:", round(n_eff, 1), "\n")
```
