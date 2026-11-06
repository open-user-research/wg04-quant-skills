# WG-04: Quantitative Analysis & Survey Research Skills

Open-source AI skills (`SKILL.md` packages) for quantitative UX research and survey methodology, developed through **Open User Research (OUR.ai) Working Group 04**.

## Skills in This Repository

| Skill | Status | Directory | Description |
| --- | --- | --- | --- |
| **Survey Suitability Gate** | `v0.3.1-draft` (portable prototype awaiting behavioral validation) | [`survey-suitability-gate/`](survey-suitability-gate/) | Refines a proposed UX survey brief and assesses whether a survey can support its intended claim before questionnaire drafting begins. |
| **Survey Question Critic & Co-Creator** | Specification in progress | `survey-question-critic/` *(planned)* | Reviews an existing survey, rewrites individual items, or drafts questionnaires grounded in psychometric and UX measurement principles. |
| **Pre-Analysis Plan & Measurement Strategy** | Specification in progress | `pre-analysis-plan/` *(planned)* | Connects research goals to constructs, measures, and anticipated analysis before fielding. |
| **Sampling & Power Coach** | Specification in progress | `sampling-and-power/` *(planned)* | Evaluates sampling frames, coverage, Survey Viability, and multi-variable power across segments. |

---

## `survey-suitability-gate` (v0.3.1-draft)

This portable package implements an adaptive intake and explicit decision gate (`PLAN_SURVEY`, `PLAN_WITH_CONDITIONS`, `MIXED_METHOD`, `OTHER_APPROACH`, or `CLARIFY`) following the [Agent Skills specification](https://agentskills.io/specification).

### Package Structure

```text
survey-suitability-gate/
├── SKILL.md
├── references/
│   ├── decision-rules.md
│   ├── source-register.md
│   ├── output-contract.md
│   └── examples.md
└── evals/
    ├── cases.md
    └── rubric.md
```

### How to Test & Review

We are actively looking for reviewers to test `survey-suitability-gate` against the 15 candidate cases in [`survey-suitability-gate/evals/cases.md`](survey-suitability-gate/evals/cases.md) (especially cases `C13`–`C15`) or against de-identified research briefs:
1. Load `survey-suitability-gate/` in an Agent Skills host (e.g., Claude, Antigravity, Cursor, Codex).
2. Run a de-identified brief or candidate case from `evals/cases.md` (withholding `evals/rubric.md` from the model).
3. Score or critique the output against `evals/rubric.md` and your own methodological judgment, and share the prompt, model output, and feedback via a GitHub issue.

## License & Attribution

- **Skills written as text, references, evaluation cases, and documentation:** © 2026 Carl J. Pearson and WG-04 contributors. Developed through Open User Research (OUR.ai), WG-04. Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
- **Code or scripts:** Licensed under the [MIT License](LICENSE).
