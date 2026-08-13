# 📌 FlyRank ML Internship — Submissions Overview & Index

Welcome to the **Submissions Overview** index for this repository. This directory contains complete breakdowns and key learnings for every completed track assignment.

---

## 🚀 Completed Submissions Index

| # | Assignment / Phase | Dedicated Detail File | Notebook / Implementation File | Simple Summary & Core Learning |
|---|---|---|---|---|
| **1** | **Phase: Setup (Week 1 & 2 Starter Notebooks)** | 📄 [submission_01_setup_notebooks.md](submissions/submission_01_setup_notebooks.md) | [`notebooks/01_first_look_and_discovery.ipynb`](notebooks/01_first_look_and_discovery.ipynb)<br>[`notebooks/02_your_first_readable_model.ipynb`](notebooks/02_your_first_readable_model.ipynb) | Ran baseline pipeline, ML beat hand-rule by 3x (Precision@50: 0.740 vs 0.240), tested SEO beliefs, feature leakage, and client-holdout validation. |
| **2** | **Week 1: Research Question & Problem Framing** | 📄 [submission_02_week1_research_question.md](submissions/submission_02_week1_research_question.md) | [`work/notebooks/w01_research_question.ipynb`](work/notebooks/w01_research_question.ipynb) | Selected **Lane 2: Refresh Opportunity Scoring**, framed decision/action workflow, backed strategy with 13,152 declining visible pages, set claim boundaries. |
| **3** | **Phase: Setup (AI Workflow Audit & Toolkit Setup)** | 📄 [submission_03_workflow_audit.md](submissions/submission_03_workflow_audit.md) | N/A (Documentation & Setup) | Audited 12 weekly tasks across AI spectrum (3 'Just Me'), configured Claude Project with custom persona/goals, completed Anthropic Academy Module 1, and set target task success criteria. |

---

## 📑 Summary of Deliverables & What Was Learned

### 🔹 [Submission 1 — Setup & Starter Notebooks](submissions/submission_01_setup_notebooks.md)
* **What Was Built:** Executed baseline ML pipeline (`scripts/run_all.py`), built decision trees, and executed "Your Turn" discovery cells in Notebooks 01 and 02.
* **What I Learned:**
  1. **ML vs. Rules:** ML models capture non-linear feature interactions that fixed hand-written rules miss (~3x Precision@50 lift).
  2. **Precision@K Metric:** Evaluating top-50 recommendations matches real operational capacity.
  3. **Feature Leakage:** Target-derived columns (like `trend_pct`) give fake 100% scores and must be excluded.
  4. **Data vs. Assumptions:** Popular beliefs (e.g. "longer content gets more traffic") failed empirical checks.
  5. **Client-Holdout Splits:** Grouping by `client_id` prevents model overfitting across domains.

### 🔹 [Submission 2 — Week 1 Research Question & Framing](submissions/submission_02_week1_research_question.md)
* **What Was Built:** Completed problem framing skeleton in `work/notebooks/w01_research_question.ipynb` for **Lane 2 (Refresh / Content Opportunity Scoring)** with live dataset verification.
* **What I Learned:**
  1. **Problem-First ML:** Applied ML starts with defining the human decision, concrete action, and cost of errors before modeling.
  2. **Dataset Grain:** Identifying row definition (`content_id`) is essential for accurate joins and feature engineering.
  3. **Decision-Support Systems:** ML models serve as high-confidence filters for human expert reviewers.
  4. **Backlog Quantification:** Quantified that 59.77% of active demand pages are declining to justify engineering investment.
  5. **Careful Claim Boundaries:** Clearly separating observational correlations from causal proof.

### 🔹 [Submission 3 — Setup: AI Workflow Audit & Toolkit Setup (FL-01)](submissions/submission_03_workflow_audit.md)
* **What Was Built:** Created 1-2 page Workflow Audit mapping 12 real recurring tasks, configured customized Claude Project persona/goals, enrolled in Anthropic Academy AI Fluency, defined 3 target audit tasks with measurable success metrics.
* **What I Learned:**
  1. **Spectrum of AI Interaction:** Fluency means picking the right mode (*Just Me*, *Delegate with Review*, *Collaborate*, *Fully Automate*) per task.
  2. **Human Boundaries:** High-stakes intuition (contest algorithms, user empathy, ethics) must remain strictly human.
  3. **Measurable Success Definitions:** Setting strict criteria for FL-02 to FL-04 target tasks ensures high engineering rigor.


---

## 🛠️ Repository Folder Map

```text
flyrank-ml-internship-starter/
├── SUBMISSION_OVERVIEW.md                          <-- You are here (Submissions index & summary)
├── submissions/
│   ├── submission_01_setup_notebooks.md            <-- Detailed Submission 1 breakdown & learnings
│   └── submission_02_week1_research_question.md    <-- Detailed Submission 2 breakdown & learnings
├── notebooks/
│   ├── 01_first_look_and_discovery.ipynb           <-- Executed: Pipeline, discoveries, your turn
│   └── 02_your_first_readable_model.ipynb          <-- Executed: Decision tree, leakage, your turn
└── work/
    └── notebooks/
        └── w01_research_question.ipynb             <-- Executed: Week 1 framing & live dataset metrics
```
