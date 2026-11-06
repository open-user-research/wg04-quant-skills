# Module 2 · Sampling, Feasibility, Weighting & Power Coach

Use this module to plan sampling strategy, audit recruitment yield using the Survey Viability Score (`SV`), calculate in-product intercept exposure and traffic allocation, account for survey weighting and Design Effects (`DEFF`), and run **multi-variable power and precision checks across every planned variable and segment**—not just a single headline metric.

---

## 1. Core Principles of Survey Sampling & Power

1. **Audit every variable and segment, not just the headline test.** Because power and precision calculations are fast to run, compute required `n`, Minimum Detectable Effect (`MDE`), and confidence interval half-widths across *all* primary outcomes, subgroup cross-tabs, and planned comparisons. A sample of `N = 400` that powers an aggregate comparison at `80%` may leave a critical 15% user segment with `n = 60` and severe underpowering.
2. **Never default blindly to `N = 384` or `400`.** The classic `N = 384` rule only gives a `±5%` margin of error for a single binary proportion at `p = .50` in a simple random sample. Between-group comparisons, rare incidences, ordinal/continuous scales, multi-arm experiments, and weighted samples have completely different sample requirements.
3. **Separate sample size from sample composition.** Sampling uncertainty (`SE`) shrinks with `1 / sqrt(n)`. Coverage gaps and nonresponse bias do not shrink as `n` increases (Valliant, Dever, & Kreuter, 2018; Groves et al., 2009).
4. **Never treat repeated observations from one respondent as independent `N`.** If 100 respondents each rate 5 features, the independent respondent sample size is `N = 100` (with within-subject correlation), never `N = 500`.

---

## 2. Recruitment Yield & The Survey Viability Score (`SV`)

Before promising a sample target to stakeholders, verify whether the reachable sampling frame and delivery channel can actually produce that yield.

### A. Invitation Pool & Yield Accounting
For a known invitation pool (e.g., email list or CRM/SQL pull):
1. **Allowed Unique Invitations (`N_invite`):** Start with eligible units in the frame, then subtract survey cooldowns, holdout reserves, and opt-outs. Remove overlapping exclusions only once.
2. **Expected Usable Completes (`n_actual`):**
   $$n_{\text{actual}} = N_{\text{invite}} \times \text{Usable-Completion Yield}$$
   - Check the denominator of every supplied rate. If "response rate" already includes eligibility and completion, do not multiply by completion rate a second time. When rates are separate conditional probabilities:
     $$\text{Usable Yield} = P(\text{Delivered}) \times P(\text{Click/Start} \mid \text{Delivered}) \times P(\text{Eligible} \mid \text{Start}) \times P(\text{Complete} \mid \text{Eligible}) \times P(\text{Pass Quality Screen} \mid \text{Complete})$$
3. **Evaluate Low / Base / High Scenarios:** Report a plausible range of expected completes based on historical team response rates or explicitly labeled sensitivity assumptions.

### B. Survey Viability Score (`SV`) & Sensitivity Multiplier
Define the **Survey Viability Score** (Pearson, 2025, 2026) as the ratio of expected usable completes (`n_actual`) to the target analytic sample (`n_planned`):

$$SV = \frac{n_{\text{actual}}}{n_{\text{planned}}}$$

Because standard errors scale with $1 / \sqrt{n}$, falling short of (or exceeding) the planned sample changes the Minimum Detectable Effect (`MDE`) and confidence interval width by the **Sensitivity Multiplier**:

$$\text{Sensitivity Multiplier} = \frac{\text{MDE}_{\text{actual}}}{\text{MDE}_{\text{planned}}} = \frac{1}{\sqrt{SV}}$$

When the planned sample `n_planned` was designed for target power $1 - \beta$ at two-sided significance level $\alpha$, the conditional power at `SV` is approximately:

$$\text{Power}(SV) \approx \Phi\left(\sqrt{SV} \cdot (z_{1 - \alpha/2} + z_{1 - \beta}) - z_{1 - \alpha/2}\right)$$

*(For two-sided $\alpha = .05$ and planned power $.80$, $z_{1-\alpha/2} \approx 1.96$ and $z_{1-\beta} \approx 0.84$, so $z_{1-\alpha/2} + z_{1-\beta} \approx 2.80$.)*

| Survey Viability (`SV`) | Expected vs. Planned Sample | MDE / CI Width Multiplier (`1 / √SV`) | Approximate Power (if planned at `.80`, $\alpha = .05$) | Planning Interpretation |
| ---: | ---: | ---: | ---: | :--- |
| **1.25** | 125% | **0.89×** | ~88% | Buffer above target; MDE is ~11% smaller |
| **1.00** | 100% | **1.00×** | 80% | Matches target in expectation (no buffer for variance) |
| **0.80** | 80% | **1.12×** | ~71% | Manageable penalty: MDE increases by ~12% |
| **0.50** | 50% | **1.41×** | ~51% | Substantial penalty: MDE is ~41% larger (`coin-flip` power for planned effect) |
| **0.25** | 25% | **2.00×** | ~29% | Severe penalty: MDE doubles; only large effects are detectable |

> **Scope limits of `SV`:** `SV >= 1.0` means expected responses meet the target in expectation, not a guarantee of realized `n`, representative coverage, or construct validity. Furthermore, `SV` does not validate whether `n_planned` was chosen well in the first place—always verify `n_planned` via the power/precision formulas below.

---

## 3. In-Product / Embedded Survey Exposure & Traffic Allocation

For in-product intercepts, micro-surveys, or post-workflow prompts, connect product traffic directly to fielding duration and exposure rates:

$$n_{\text{daily}} = \text{Eligible Daily Unique Users} \times \text{Trigger Rate} \times \text{Intercept Exposure Rate (\%)} \times \text{View-to-Complete Yield}$$

$$\text{Fielding Days Required} = \frac{n_{\text{planned}} \times \text{DEFF}}{n_{\text{daily}}}$$

### Traffic Allocation Rules
1. **Day-of-Week Cyclicality:** Field in-product surveys across full **7-day multiples** (or weight/stratify by day of week) whenever weekday vs. weekend user behavior differs.
2. **Throttling & Cooldowns:** If daily traffic far exceeds what is needed, lower the **Intercept Exposure Rate** (e.g., sample `5%` or `10%` of eligible triggers at random) rather than exhausting the entire user pool on Day 1 and capturing only a single day's conditions or heaviest daily active users.
3. **Frequency Bias in Intercepts:** Users who visit the product every day have a much higher probability of encountering an event-triggered intercept than weekly or monthly users. Either sample at the **user ID level** over a fixed window or apply inverse-inclusion / engagement weights.

---

## 4. Survey Weighting & Design Effects (`DEFF`)

In UX research, respondents almost never match the population proportions on engagement, tenure, or geography—engaged users respond at much higher rates (Pearson, *Survey Weighting for UX Research*; Valliant et al., 2018).

### A. Choosing Weighting Strategy & Variables
- **Prioritize behavioral and product-relevant variables over arbitrary demographics:** In tech and product research, log-derived **usage tenure**, **engagement/activity tier**, **account/plan type**, **platform (iOS/Android/Web)**, and **country** strongly relate to both response propensity and UX attitudes. Demographic variables (age/gender) rarely drive software usability directly unless tied to a specific mechanism.
- **When NOT to weight:**
  1. Randomized between-subjects experiments (e.g., prototype A/B tests where random assignment balances covariates across arms, unless estimating population-wide marginal totals).
  2. When no trustworthy population benchmark exists (e.g., uncalibrated third-party opt-in panels).
- **Post-Stratification vs. Calibration/Raking:**
  - **Post-stratification (`survey::postStratify`)** uses full cross-classified population cell counts (e.g., `Tenure × Engagement Tier` from a `GROUP BY` SQL pull). It folds design and non-response adjustments into a single step when `Sampling Frame == Population`, but requires respondents in every cell (`n_cell >= 1`, ideally `>= 10–20` for stability).
  - **Raking / Iterative Proportional Fitting (`survey::rake`)** matches marginal population totals when full cross-tabs are unavailable or when cross-cells are sparse.
- **Weight Trimming:** Extreme weights inflate variance. Inspect weight distributions (`min`, `median`, `max`, ratio of `max/min`) and consider trimming extreme weights (e.g., capping at `3.5×` to `5×` the median weight) while checking bias-variance trade-offs.

### B. Accounting for Kish's Design Effect (`DEFF`) in Sample Planning
Unequal weights increase sampling variance. Quantify this variance inflation using **Kish's Design Effect (`DEFF`)**:

$$\text{DEFF} = 1 + \text{CV}(w)^2 = 1 + \left(\frac{s_w}{\bar{w}}\right)^2$$

where $\bar{w}$ and $s_w$ are the mean and standard deviation of the weights.
- **Effective Sample Size (`n_eff`):**
  $$n_{\text{eff}} = \frac{n_{\text{actual}}}{\text{DEFF}}$$
- **Pre-Fielding Sample Size Inflation:** If a study will be weighted (or uses disproportionate stratified oversampling), inflate the unweighted target sample size by the anticipated `DEFF` (typically `1.15` to `1.50` for moderate raking/post-stratification; `1.50` to `2.50+` for aggressive oversampling):
  $$n_{\text{target, weighted}} = n_{\text{unweighted}} \times \text{DEFF}$$

---

## 5. Multi-Variable Power & Precision Formulas

Always distinguish **Precision Planning** (estimating a quantity within a target confidence interval half-width `±MOE`) from **Power Planning** (detecting a difference or effect of size $\Delta$ with probability $1 - \beta$ at significance level $\alpha$).

### A. Precision Planning (Single-Group Estimation)
1. **Binary Proportion (`p`):**
   $$n = \frac{z_{1-\alpha/2}^2 \cdot p(1 - p)}{\text{MOE}^2} \times \text{DEFF}$$
   *(Use Adjusted-Wald / Wilson intervals in R for reporting, especially when `n` is small or `p` is near `0` or `1`.)*
2. **Continuous or Multi-Item Scale Mean (`SD = \sigma`):**
   $$n = \left(\frac{z_{1-\alpha/2} \cdot \sigma}{\text{MOE}}\right)^2 \times \text{DEFF}$$

### B. Hypothesis Testing & MDE Across Common Designs (Two-Sided $\alpha$, Power $1 - \beta$)
Let $Z = z_{1-\alpha/2} + z_{1-\beta}$ (for $\alpha = .05, 1-\beta = .80$, $Z \approx 2.80$; for $1-\beta = .90$, $Z \approx 3.24$).

1. **Two Independent Means (Equal allocation $n$ per group, total $N = 2n$):**
   - Required per group for standardized effect $d = |\mu_1 - \mu_2| / \sigma$:
     $$n_{\text{per group}} \approx \frac{2 \cdot Z^2}{d^2} \times \text{DEFF}$$
   - Minimum Detectable Effect (`MDE`) given $n_1, n_2$ and `DEFF`:
     $$\text{MDE}_{\text{raw}} = Z \cdot \sigma \cdot \sqrt{\text{DEFF} \cdot \left(\frac{1}{n_1} + \frac{1}{n_2}\right)}$$
2. **Paired / Within-Subjects Means ($n$ respondents, correlation $r$ between measures):**
   $$n_{\text{paired}} \approx \frac{Z^2 \cdot 2(1 - r)}{d_z^2} \times \text{DEFF}$$
3. **Two Independent Proportions ($p_1$ vs. $p_2$, difference $\Delta = |p_1 - p_2|$):**
   $$n_{\text{per group}} \approx \frac{Z^2 \cdot \left[p_1(1 - p_1) + p_2(1 - p_2)\right]}{\Delta^2} \times \text{DEFF}$$
   $$\text{MDE}_{\Delta} \approx Z \cdot \sqrt{\text{DEFF} \cdot \bar{p}(1 - \bar{p}) \cdot \left(\frac{1}{n_1} + \frac{1}{n_2}\right)}$$
4. **Ordinal Likert Scale (Whitehead's Proportional-Odds Formula vs. Naive T2B Dichotomization):**
   - Analyzing a `K`-category ordinal scale with proportional odds (`ordinal::clm`) is substantially more efficient than dichotomizing into Top-2-Box before testing. By Whitehead (1993), for category proportions $\pi_1, \dots, \pi_K$ and log-odds ratio $\theta = \log(\text{OR})$:
     $$n_{\text{per group, ordinal}} \approx \frac{6 \cdot Z^2}{\theta^2 \cdot \left(1 - \sum_{k=1}^K \pi_k^3\right)} \times \text{DEFF}$$
   - A 5- or 7-point ordinal model typically requires **20% to 35% fewer respondents** than a naive binary proportion test to achieve the same power for an equivalent shift in Top-2-Box!

---

## 6. Required Outputs from the Sampling & Power Coach

When running Module 2, return these five deliverables:

1. **Multi-Variable Power & Precision Audit Table:**
   A table covering *every* planned primary/secondary variable and segment comparison:

| Variable / Test | Analysis Level (`Aggregate` / `Segment`) | Planned Test & Scale | Assumed Baseline / `SD` | Target `n` (Raw) | Anticipated `DEFF` | Effective `n` (`n_eff`) | Achievable `MDE` (at 80% Power, $\alpha=.05$) | 95% CI Half-Width (`±MOE`) | Risk Flag (`Green` / `Amber` / `Red`) |
| :--- | :--- | :--- | :--- | ---: | ---: | ---: | :--- | :--- | :--- |
| `Q1: Overall CSAT (T2B)` | Aggregate (`All Users`) | Ordinal logit (`5-pt`) → derived T2B | `65%` T2B | 600 | 1.20 | 500 | `±4.8` pts (1 group) | `±3.8%` | **Green** |
| `Q1: CSAT by Segment` | `New` (20%) vs. `Established` (80%) | 2-group ordinal contrast | `60%` vs. `70%` | 120 vs. 480 | 1.20 | 100 vs. 400 | `13.5` pt lift (`OR ~ 1.75`) | `±8.5%` in New | **Amber** (powered only for medium-large segment gaps) |
| `Q4: Enterprise Admin Flow` | `Admins` only (5% incidence) | Binary proportion | `50%` | 30 | 1.20 | 25 | `±26%` vs. non-admins | `±19.6%` | **Red** (Underpowered; oversample Admins or treat as descriptive only) |

2. **Survey Viability (`SV`) & Sensitivity Forecast:**
   - Show unique invitation pool (`N_invite`), assumed completion yield, expected completes (`n_actual`), `SV = n_actual / n_planned`, and the MDE sensitivity multiplier (`1 / sqrt(SV)`) across Low / Base / High yield scenarios.
3. **Exposure Rate & Traffic Allocation Plan (for In-Product Surveys):**
   - Daily eligible traffic, recommended trigger/exposure throttling %, expected daily completes, and total fielding days (in 7-day multiples).
4. **Weighting & Stratification Recommendation:**
   - Recommended weighting variables (e.g., tenure, engagement tier, country), whether to use disproportionate stratified sampling (e.g., oversampling rare critical segments like `Enterprise Admins` and applying design weights), and expected `DEFF`.
5. **Plain-Language Stakeholder Risk Statement:**
   - Translate statistical limits into concrete decision terms for PMs and executives (e.g., *"With 500 expected responses and a 1.20 weighting design effect, we can reliably detect a 6-point shift in overall satisfaction, but in the Enterprise subgroup (`n = 35`) we can only detect shifts of 18+ points. If the Enterprise decision requires finer precision, we must oversample Enterprise accounts via email rather than relying on random in-app intercepts."*).
