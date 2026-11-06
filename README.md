# WG-04: Quantitative Analysis & Survey Research Skills

Open-source AI skills (`SKILL.md` packages) for quantitative UX research and survey methodology, developed through **Open User Research (OUR.ai) Working Group 04**.

## Skills in This Repository

| Skill | Status | Directory | Description |
| --- | --- | --- | --- |
| **Survey Planning & Methodology Skill (Unified 4-Module Package)** | `v1.0.0` (end-to-end package with mocked evaluation runs across `C13`–`C15` and experimental checkout) | [`survey-planning/`](survey-planning/) | Integrates Stage 0 (Suitability & Method Routing Gate), Module 1 (Measurement Strategy & Pre-Analysis Plan with R code), Module 2 (Sampling, Survey Viability `SV`, Weighting `DEFF`, & Multi-Variable Power Coach), and Module 3 (Question Critic, Co-Creator, & Two-Stage Pretesting). |
| **Survey Suitability Gate (Standalone)** | `v0.3.1-draft` (portable prototype awaiting cross-model behavioral validation) | [`survey-suitability-gate/`](survey-suitability-gate/) | Refines a proposed UX survey brief and assesses whether a survey can support its intended claim before questionnaire drafting begins. |

---

## 1. `survey-planning/` (Unified 4-Module Skill, `v1.0.0`)

Combines the four WG-04 pre-fielding specifications into a single progressive-disclosure Agent Skill package:
- **Stage 0 · Suitability & Method Routing Gate** ([`references/suitability-and-routing.md`](survey-planning/references/suitability-and-routing.md))
- **Module 1 · Measurement Strategy & Pre-Analysis Plan** ([`references/measurement-and-preanalysis.md`](survey-planning/references/measurement-and-preanalysis.md))
- **Module 2 · Sampling, Feasibility, Weighting & Power Coach** ([`references/sampling-weighting-and-power.md`](survey-planning/references/sampling-weighting-and-power.md))
- **Module 3 · Survey Question Critic, Co-Creator & Pretesting** ([`references/question-critic-and-pretesting.md`](survey-planning/references/question-critic-and-pretesting.md))
- **Methodological Source Register** ([`references/source-register.md`](survey-planning/references/source-register.md))
- **Evaluation Suite & Mocked Runs** ([`evals/cases.md`](survey-planning/evals/cases.md), [`evals/rubric.md`](survey-planning/evals/rubric.md), [`evals/mock_eval_results.md`](survey-planning/evals/mock_eval_results.md))

---

## 2. `survey-suitability-gate/` (Standalone Gate, `v0.3.1-draft`)

This portable package implements an adaptive intake and explicit decision gate (`PLAN_SURVEY`, `PLAN_WITH_CONDITIONS`, `MIXED_METHOD`, `OTHER_APPROACH`, or `CLARIFY`) following the [Agent Skills specification](https://agentskills.io/specification), along with 15 candidate evaluation cases (`C1`–`C15`).

### How to Test & Review

We are actively looking for reviewers to test `survey-planning/` and `survey-suitability-gate/` against candidate cases (`C13`–`C15`) or de-identified research briefs:
1. Load `survey-planning/` or `survey-suitability-gate/` in an Agent Skills host (Claude, Antigravity, Cursor, Codex).
2. Run a de-identified brief or candidate case from `evals/cases.md` (withholding `evals/rubric.md` from the model).
3. Score or critique the output against `evals/rubric.md` and your own methodological judgment, and share the prompt, model output, and feedback via a GitHub issue or in the WG-04 Circle space.

## License & Attribution

- **Skills written as text, references, evaluation cases, and documentation:** © 2026 Carl J. Pearson, Alex Guliaeva, Dermina Vasc, Rottem Sagi, Nicole Bonoff, Vicky Chen, Jeff Berg, Owen Hughes, Suyi Leong. Developed through Open User Research (OUR.ai), WG-04. Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
- **Code or scripts:** Licensed under the [MIT License](LICENSE).
