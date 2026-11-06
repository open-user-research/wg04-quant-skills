# WG04 Survey Planning Skill — Evaluation Cases

Use these test briefs to evaluate the `survey-planning` skill across Stage 0 (Suitability & Routing) and Modules 1–3 (Measurement & Pre-Analysis, Sampling/Weighting/Power, and Question Critic & Pretesting).

---

## Case 1 · Mixed-Method Routing & Unknown Categories (Book-Grounded Case C13)

**User Prompt:**
> "Our product telemetry shows how many active accounts completed a CSV export last month, and completion dropped 14%. Leadership wants us to launch a survey this week asking users why exporting feels difficult and which export bug hurt them most, though we haven't done qualitative research on the new export flow yet. Can you draft the survey?"

**Expected Skill Behavior:**
1. **Stage 0 Disposition (`MIXED_METHOD`):**
   - Separate the two implicit claims: (a) export counts/drop magnitude are already covered by validated product logs (do not re-ask usage counts via recall survey), and (b) discovering *why* exporting feels difficult when error categories are unknown requires exploratory qualitative research or usability observation *before* a standardized closed-ended prevalence survey (Sauro & Lewis, 2024, Ch. 1; Jarrett, 2021, Ch. 1; Pearson, 2026).
   - Also flag that if leadership wants to prove a recent release *caused* the 14% drop, a retrospective survey cannot isolate causal impact on its own.
2. **Integration Point (Ladner, 2019):**
   - Specify an **exploratory sequential route**: (Step 1) Observe 6–8 users attempting exports or review support tickets/session replays + open-ended intercept prompts to identify the actual failure modes; (Step 2) Use those discovered failure modes to construct mutually exclusive closed-ended response options if leadership still needs prevalence estimates across segments.
3. **Conditional Draft / Stop:**
   - Offer a short 2–3 question post-export intercept (Ease `SEQ` + open-ended diagnostic prompt) if immediate in-flow feedback is needed, while holding back a premature closed-ended "bug checklist" survey.

---

## Case 2 · Abstract Construct, Missing Pretesting & Active-Only Coverage Trap (Combined Cases C14 & C15)

**User Prompt:**
> "We want to estimate how much all of our Q3 customers—including users who churned last month—trust our new AI coding assistant, and compare Free vs. Pro vs. Enterprise Admin segments. We'll email our currently active monthly users (`N_invite = 15,000`, expected usable completion yield `6%`) with a web survey asking: `'How much do you agree: I trust the AI assistant and find its suggestions accurate? (1 = Strongly Disagree to 5 = Strongly Agree, required)'`. We need `500` total responses and we'll just check that the survey link works before launching."

**Expected Skill Behavior:**
1. **Stage 0 Disposition (`PLAN_WITH_CONDITIONS`):**
   - **Coverage Blocker (C15):** The target population includes *all Q3 customers including recent churners*, but the sampling frame only reaches *currently active users*. Even though expected yield (`15,000 × 0.06 = 900` completes) exceeds the aggregate `500` target (`SV = 1.80`), sampling error reduction never fixes missing churner coverage (Sauro & Lewis, 2024, Ch. 2). Either expand the email frame to include churned Q3 accounts (and weight for differential nonresponse) or narrow the claim to active users.
2. **Module 1 & Module 3 Item Critique (C14):**
   - **Construct ambiguity (`Critical`/`Major`):** "Trust" is abstract and unanchored. Define what aspect of trust matters to the product decision (e.g., confidence in code correctness, privacy/data security, or predictability) and anchor to a concrete reference period (*"In the past 14 days..."*).
   - **Double-barreled & Agree/Disagree bias (`Major`):** *"I trust the AI assistant and find its suggestions accurate"* combines trust and accuracy in one item and uses an Agree/Disagree format prone to acquiescence bias. Split into two construct-specific 5-point bipolar/unipolar items.
   - **Forced response without `N/A` (`Major`):** Requiring an answer without a `"Have not used the AI assistant"` exit or skip logic forces non-users into the midpoint (`3 = Neither`).
3. **Module 2 Multi-Variable Power & Viability Audit:**
   - Aggregate yield is `900` (`SV = 1.80`, sensitivity multiplier `0.75×`), but audit the **Enterprise Admin** subgroup: if Enterprise Admins are only `3%` of active users (`900 × 0.03 = 27` expected completes) and weighting introduces `DEFF = 1.25` (`n_eff = 21.6`), the study is severely underpowered (`Red` flag) for Enterprise Admin comparisons unless Enterprise Admins are disproportionately oversampled.
4. **Pretesting Requirement (C14):**
   - Explicitly separate **Cognitive Testing** (e.g., rapid unmoderated think-aloud with 4–6 users across tiers to test how they interpret "trust") from an **Operational Pilot** (soft launch to 30–50 users to verify routing, `% N/A`, and the R analysis script). A link check does not test respondent interpretation.

---

## Case 3 · End-to-End Survey Plan: Measurement Map, Pre-Analysis R Code & Ordinal Top-2-Box

**User Prompt:**
> "We are running a randomized in-product A/B experiment (`Control` vs. `Simplified Checkout`) where users are randomly assigned at checkout. Beyond logged checkout conversion, we want an embedded post-checkout survey to test whether `Simplified Checkout` improves perceived checkout ease (action threshold: at least a `+6` percentage-point lift in Top-2-Box ease) and whether it reduces perceived payment confusion, broken out by `New` (`30%`) vs. `Returning` (`70%`) buyers. Daily eligible checkout traffic is `10,000` users per arm (`20,000` total), and we expect a `15%` view-to-complete rate on a 3-question intercept. Give us the full measurement plan, sampling/exposure & multi-variable power plan, questionnaire, and pre-analysis R code."

**Expected Skill Behavior:**
1. **Stage 0 Suitability (`PLAN_SURVEY`):**
   - Because treatment is randomized (`Control` vs. `Simplified Checkout`), a survey *can* measure causal treatment effects on perceived ease and confusion—provided the team checks for **differential survey nonresponse** across the two experiment arms (Bakhshi, 2026; Navarro, Ch. 2).
2. **Module 1 Measurement & Pre-Analysis Plan:**
   - Map `RQ1 (Perceived Ease)` to post-task `SEQ` (7-point scale) or 5-point ease scale, and `RQ2 (Payment Confusion)` to a construct-specific item + optional targeted open-end.
   - Specify **Ordinal Cumulative Logit (`ordinal::clm`) + Derived Top-2-Box** (`emmeans(..., mode = "prob")`) rather than dichotomizing the raw scale before testing (Pearson, 2026, *Deriving Top-2-Box from Ordinal Models*).
   - Note that because this is a randomized experiment, design weights are not required for internal validity unless differential nonresponse occurs between arms or population marginal totals are needed.
3. **Module 2 Sampling, Exposure & Multi-Variable Power Coach:**
   - Calculate sample size needed per arm to detect a `+6` percentage-point lift in Top-2-Box (from e.g. `70%` to `76%`) both overall and within the smaller `New Buyers (30%)` subgroup.
   - Calculate in-product **Intercept Exposure Rate** over a full **7-day cycle** so traffic is throttled evenly across days of the week rather than burning through the entire sample in 4 hours on a Tuesday.
4. **Module 3 Questionnaire & Pretesting:**
   - Keep the intercept to `<= 3` items (`< 90` seconds), place overall ease (`SEQ`) *before* specific payment-confusion items to prevent priming (Tourangeau & Rasinski, 1988), and provide the ready-to-run R script.
