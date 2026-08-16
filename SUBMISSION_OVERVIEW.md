# 📌 FlyRank ML Internship — Submissions Overview & Index

Welcome to the **Submissions Overview** index for this repository. This directory contains complete breakdowns and key learnings for every completed track assignment.

---

## 🚀 Completed Submissions Index

| # | Assignment / Phase | Dedicated Detail File | Notebook / Implementation File | Simple Summary & Core Learning |
|---|---|---|---|---|
| **1** | **Phase: Setup (Week 1 & 2 Starter Notebooks)** | 📄 [submission_01_setup_notebooks.md](submissions/submission_01_setup_notebooks.md) | [`notebooks/01_first_look_and_discovery.ipynb`](notebooks/01_first_look_and_discovery.ipynb)<br>[`notebooks/02_your_first_readable_model.ipynb`](notebooks/02_your_first_readable_model.ipynb) | Ran baseline pipeline, ML beat hand-rule by 3x (Precision@50: 0.740 vs 0.240), tested SEO beliefs, feature leakage, and client-holdout validation. |
| **2** | **Week 1: Research Question & Problem Framing** | 📄 [submission_02_week1_research_question.md](submissions/submission_02_week1_research_question.md) | [`work/notebooks/w01_research_question.ipynb`](work/notebooks/w01_research_question.ipynb) | Selected **Lane 2: Refresh Opportunity Scoring**, framed decision/action workflow, backed strategy with 13,152 declining visible pages, set claim boundaries. |
| **3** | **Phase: Setup (AI Workflow Audit & Toolkit Setup)** | 📄 [submission_03_workflow_audit.md](submissions/submission_03_workflow_audit.md) | N/A (Documentation & Setup) | Audited 12 weekly tasks across AI spectrum (3 'Just Me'), configured Claude Project with custom persona/goals, completed Anthropic Academy Module 1, and set target task success criteria. |
| **4** | **Phase: Setup (Portfolio Sitemap & Claude Tutor Setup)** | 📄 [submission_04_portfolio_sitemap.md](submissions/submission_04_portfolio_sitemap.md) | N/A (Documentation & Design) | Designed lean portfolio sitemap around single proof claim & target action, setup Claude Portfolio Tutor Project, pressure-tested sitemap with AI, and refactored layout to single-page scroll. |
| **5** | **Phase: Setup (What Are You Proving? Proof Statement)** | 📄 [submission_05_proof_statement.md](submissions/submission_05_proof_statement.md) | N/A (Documentation & Strategy) | Authored hyper-focused 1-paragraph proof statement (claim + person + action), defined one-line "why", and passed AI interview pressure-testing. |
| **6** | **Phase: Foundations (ML-03 Task Framing)** | 📄 [submission_06_ml_task_framing.md](submissions/submission_06_ml_task_framing.md) | [`work/notebooks/w02_ml_task_framing.ipynb`](work/notebooks/w02_ml_task_framing.ipynb) | Framed Lane 2 as Ranking / Scoring problem, defined observed target proxy ($\Delta \text{Imp}_{\text{rel}} < -15\%$), defended Precision@50, verified 22,006-row slice, and demonstrated multi-signal ML superiority over static rules (+10.00% gain). |

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

### 🔹 [Submission 4 — Setup: Portfolio Sitemap & Claude Tutor Setup](submissions/submission_04_portfolio_sitemap.md)
* **What Was Built:** Sketched visual Mermaid sitemap, defined proof statement and target conversion action, configured `FlyRank-Portfolio-Tutor` Claude Project, and ran pressure-test prompt to refine sitemap layout.
* **What I Learned:**
  1. **Conversion Funnel Design:** Every page must directly support the core proof claim and target booking CTA.
  2. **Friction Reduction:** Refactored from multi-page navigation to single-page scroll layout based on Claude pressure-test feedback.
  3. **Continuous AI Mentorship:** Setting up a dedicated Claude Tutor Project enables real-time architectural critiques across the 8-week build.

### 🔹 [Submission 5 — Setup: Proof Statement & Core Focus](submissions/submission_05_proof_statement.md)
* **What Was Built:** Wrote one-paragraph proof statement answering claim, person, and action, defined one-line "why", and documented AI thinking partner interview refinements.
* **What I Learned:**
  1. **Single-Claim Discipline:** Avoiding generic lists of skills ("X and Y and Z") forces sharp differentiation.
  2. **Audience Specificity:** Targeting a concrete technical lead ensures every metric (Precision@50, client holdouts) resonates.
  3. **Proving Beyond CVs:** A portfolio's sole job is to prove practical engineering judgment that static resumes cannot convey.

### 🔹 [Submission 6 — Phase: Foundations (ML-03 Task Framing)](submissions/submission_06_ml_task_framing.md)
* **What Was Built:** Completed executed notebook `work/notebooks/w02_ml_task_framing.ipynb` mapping Lane 2 onto ML ranking/scoring loop, defined observed target proxy ($\Delta \text{Imp}_{\text{rel}} < -15\%$), defended Precision@50, inspected 22,006-row active demand slice dataframe, and proved multi-signal ML superiority (+10.00% Precision@50 gain over static rule).
* **What I Learned:**
  1. **Outcome-Based Labels:** ML targets must measure observed search console outcomes in later time windows rather than memorizing circular product tags.
  2. **Operational Metric Alignment:** Precision@50 directly measures editorial Return-on-Investment for capacity-constrained teams.
  3. **Non-Linear Interactions:** Fixed rules fail on position-CTR non-linearities, whereas multi-signal ML scoring captures non-linear feature combinations effectively.

---

## 🛠️ Repository Folder Map

```text
flyrank-ml-internship-starter/
├── SUBMISSION_OVERVIEW.md                          <-- You are here (Submissions index & summary)
├── submissions/
│   ├── submission_01_setup_notebooks.md            <-- Detailed Submission 1 breakdown & learnings
│   ├── submission_02_week1_research_question.md    <-- Detailed Submission 2 breakdown & learnings
│   ├── submission_03_workflow_audit.md            <-- Detailed Submission 3 breakdown & learnings
│   ├── submission_04_portfolio_sitemap.md          <-- Detailed Submission 4 breakdown & learnings
│   ├── submission_05_proof_statement.md           <-- Detailed Submission 5 breakdown & learnings
│   └── submission_06_ml_task_framing.md            <-- Detailed Submission 6 breakdown & learnings
├── notebooks/
│   ├── 01_first_look_and_discovery.ipynb           <-- Executed: Pipeline, discoveries, your turn
│   └── 02_your_first_readable_model.ipynb          <-- Executed: Decision tree, leakage, your turn
└── work/
    └── notebooks/
        ├── w01_research_question.ipynb             <-- Executed: Week 1 framing & live dataset metrics
        └── w02_ml_task_framing.ipynb               <-- Executed: Week 2 ML task framing & target definition
```
