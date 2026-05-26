# Analytical Case Studies

Graduate-level data science case studies designed around the synthetic datasets in this repository. Each case study places you in the role of an analytics professional facing a real-world business challenge — with messy data, tight deadlines, and decisions that go beyond the model.

## How to Use

1. **Read the case narrative first.** Understand the business context, the protagonist's challenge, and the stakes before touching the data.
2. **Review the exhibits.** Each case includes supplementary materials (stakeholder memos, KPI dashboards) that provide additional context.
3. **Load the dataset.** The CSV file path is listed in each case study. Use the corresponding data dictionary for column definitions.
4. **Work through the discussion questions.** These are open-ended — there is no single correct answer. Be prepared to defend your choices.
5. **Prepare the executive deliverable.** Each case concludes with a board-level presentation or recommendation. Practice communicating technical findings to non-technical stakeholders.

## Available Case Studies

| Case Study | Industry | Dataset | Description |
|-----------|----------|---------|-------------|
| [The Quiet Exodus](marketing/marketing.md) | Marketing | 600K customers, 29 cols | Customer churn and CLV at a mid-size e-commerce company |
| [Thirty Days](healthcare/healthcare.md) | Healthcare | 500K patients, 21 cols | Hospital readmission prediction under CMS penalty pressure |
| [The Missing Signal](depression/depression.md) | Depression | 400K patients, 32 cols | Mental health triage and treatment dropout at a community network |

## Structure

Each case study folder contains:

```
<industry>/
├── <industry>.md           ← Main case narrative + discussion questions
└── exhibits/
    ├── exhibit_A.md        ← Stakeholder memo or regulatory notice
    └── exhibit_B.md        ← Organizational dashboard or KPI snapshot
```

## Companion Resources

These case studies complement (but do not replace) the existing resources in this repository:

- **Data Dictionaries** — `documentation/data_dictionaries/` — Column definitions, types, and valid ranges
- **Suggested Tasks** — `documentation/suggested_tasks/` — Additional analytical questions organized by technique

## Design Philosophy

These cases are inspired by the Harvard Business School case method but adapted for data science:

- **Narrative-driven.** Every dataset is wrapped in a story with named characters, organizational context, and real stakes.
- **Data-grounded.** Every number cited in the case is verifiable from the actual CSV on this repository.
- **Open-ended.** There are no "right answers" — students must make and defend analytical choices.
- **Ethically aware.** Each case includes a genuine ethical tension with no easy resolution.
- **Dual-target.** Each case requires both classification and regression, reflecting real-world analytics where problems come in pairs.

---

*These case studies are prepared for classroom discussion and are not intended to represent actual organizations. All characters are fictional. The datasets are synthetic and available for student analysis.*
