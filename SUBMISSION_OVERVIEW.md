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
| **7** | **Phase: Setup & AI Fluency (FL-02 Frame It As Cases)** | 📄 [submission_07_framed_cases.md](submissions/submission_07_framed_cases.md) | N/A (Documentation & AI Fluency) | Created 5-word voice card, conducted AI Q&A interview, drafted 3-beat case studies for FlyRank, CP Vault, and Campus Buddy, wrote bio/CTA copy, and included generic AI vs edited human before/after line. |
| **8** | **Phase: Setup & AI Fluency (FL-03 Prompt Ladder)** | 📄 [submission_08_prompt_ladder.md](submissions/submission_08_prompt_ladder.md) | N/A (Prompt Engineering Asset) | Built 6-run prompt ladder (V0 weak baseline + 5 single-layer iterations), documented 4 evaluation notes per step, identified honest PyTorch over-engineering failure (V3), and delivered final reusable prompt. |
| **9** | **Phase: Foundations & AI Fluency (FL-02 Prompting Fundamentals v2)** | 📄 [submission_09_prompting_fundamentals.md](submissions/submission_09_prompting_fundamentals.md) | N/A (Prompt Engineering Log) | Applied 5 named techniques (Role, Context, Few-Shot, Format, Chain-of-Thought) to Data Contract audit task, conducted honest Claude vs ChatGPT comparison, and built reusable template asset. |
| **10** | **Phase: Foundations (ML-04 Search Intelligence Data Contract)** | 📄 [submission_10_data_contract.md](submissions/submission_10_data_contract.md) | [`work/notebooks/w03_data_contract.ipynb`](work/notebooks/w03_data_contract.ipynb) | Wrote 5-part plain-words contract, ran 3 verification queries (grain uniqueness, row counts, IS TRUE availability), built 5-feature frame, and executed deliberate leakage trap (100% fake score vs 77.60% honest score). |
| **11** | **Phase: Foundations & AI Fluency (FL-04 Build Your Identity Kit)** | 📄 [submission_11_identity_kit.md](submissions/submission_11_identity_kit.md) | N/A (Design & Brand Asset) | Defined typography pairing (Plus Jakarta Sans + Inter), 4-color palette (#F8FAFC, #FFFFFF, #0F172A, #2563EB), built SVG AP monogram logo, and configured 2-line style note in Claude Project. |
| **12** | **Phase: Foundations & AI Fluency (FL-05 Curate Your Images)** | 📄 [submission_12_curate_images.md](submissions/submission_12_curate_images.md) | N/A (Visual Asset Curation) | Mapped portfolio image inventory, prioritized real captures/logs over AI stand-ins, and documented discernment rejection log cutting 3D cyber-brain fluff and fake Midjourney dashboards. |
| **13** | **Phase: Foundations & AI Fluency (FL-06 Map Content & CTAs)** | 📄 [submission_13_content_map.md](submissions/submission_13_content_map.md) | N/A (Content & Funnel Strategy) | Formulated sharp one-line claim, mapped section-by-section layout with named CTAs leading with FlyRank 88% P@50 case, and compiled honest list of proof assets still to gather. |

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

### 🔹 [Submission 7 — Phase: Setup & AI Fluency (FL-02 Frame It As Cases)](submissions/submission_07_framed_cases.md)
* **What Was Built:** Created 5-word voice card, conducted AI Q&A interview, drafted 3-beat case studies for FlyRank, CP Vault, and Campus Buddy, wrote bio/CTA copy, and included generic AI vs edited human before/after line.
* **What I Learned:**
  1. **AI as Interviewer:** Having AI interview me about real decisions extracted authentic human narratives without generic fluff.
  2. **3-Beat Case Structure:** Problem, What I Did & Decided, What Came Of It creates clear, evidence-based portfolio cases.
  3. **Voice Control:** A strict voice card ("sharp, empirical, plain, direct, evidence-first") sets clear boundaries to edit out AI resume buzzwords.

### 🔹 [Submission 8 — Phase: Setup & AI Fluency (FL-03 Prompt Ladder)](submissions/submission_08_prompt_ladder.md)
* **What Was Built:** Built 6-run prompt ladder starting from a weak V0 baseline through 5 single-layer iterations (Context, Goal, Audience, Constraints, Format), documented 4 notes per run, identified an honest PyTorch over-engineering failure (V3), and delivered a reusable prompt asset.
* **What I Learned:**
  1. **Single-Layer Isolation:** Adding exactly one layer per prompt iteration reveals precisely which instruction drove a given output improvement.
  2. **Constraints Over Persona:** Adding explicit negative constraints (no PyTorch, use scikit-learn, GroupKFold on client_id) is far more critical for code reliability than vague persona descriptions.
  3. **Honest Evaluation:** Recognizing when an added layer makes output worse (V3 PyTorch over-engineering) prevents shipping overly complex solutions.

### 🔹 [Submission 9 — Phase: Foundations & AI Fluency (FL-02 Prompting Fundamentals v2)](submissions/submission_09_prompting_fundamentals.md)
* **What Was Built:** Applied 5 named techniques (Role Assignment, Context & Motivation, Few-Shot Examples, Output Structure, Step Decomposition) to an FL-01 Data Contract audit task, conducted cross-model comparison between Claude and ChatGPT, and built a portable prompt template.
* **What I Learned:**
  1. **Step Decomposition Prevents Rushing:** Adding explicit `<thinking>` chain-of-thought logic caught schema gotchas like `avg_position = 0` before code generation.
  2. **Few-Shot Structure Control:** Providing a small YAML exemplar enforced schema syntax far more effectively than descriptive text instructions alone.
  3. **Model Strengths:** Claude excels at strict format adherence and system assertions, while ChatGPT requires stronger constraints to avoid conversational text preamble.

### 🔹 [Submission 10 — Phase: Foundations (ML-04 Search Intelligence Data Contract)](submissions/submission_10_data_contract.md)
* **What Was Built:** Completed executed notebook `work/notebooks/w03_data_contract.ipynb`, formulated 5 plain-words contract answers, executed 3 verification queries (grain probe, row count, IS TRUE availability filter), constructed 5-feature frame with availability justifications, and executed the deliberate feature leakage trap.
* **What I Learned:**
  1. **Query-Backed Verification:** Every contract assertion must be validated with executable pandas/SQL queries rather than assumed.
  2. **Availability Filter Discipline:** Filtering demand with `impressions_90d >= 100 IS TRUE` isolates active pages (22,006 rows / 73.35%) and removes zero-traffic noise.
  3. **Leakage Trap Proof:** Intentionally leaking `trend_pct` produced a fake 100.00% Precision@50 score; removing it preserved honest model performance (77.60%).

### 🔹 [Submission 11 — Phase: Foundations & AI Fluency (FL-04 Build Your Identity Kit)](submissions/submission_11_identity_kit.md)
* **What Was Built:** Defined typography pairing (Plus Jakarta Sans + Inter), 4-color palette (#F8FAFC, #FFFFFF, #0F172A, #2563EB), built SVG AP monogram logo, and configured 2-line style note in Claude Project.
* **What I Learned:**
  1. **Decide Once Discipline:** Fixing typography and color hex codes upfront prevents visual fragmentation across portfolio pages.
  2. **Data-Dense Frame:** A quiet 4-color palette ensures code blocks and Precision@50 metrics stand out as the primary visual focus.
  3. **AI Style Guardrail:** Adding a 2-line style note to standing instructions forces AI coding assistants to generate UI components matching the exact brand identity.

### 🔹 [Submission 12 — Phase: Foundations & AI Fluency (FL-05 Curate Your Images)](submissions/submission_12_curate_images.md)
* **What Was Built:** Mapped portfolio image inventory, prioritized real captures/logs over AI stand-ins, and documented discernment rejection log cutting 3D cyber-brain fluff and fake Midjourney dashboards.
* **What I Learned:**
  1. **Proof Over Polish:** Real terminal logs and Precision@50 evaluation charts build authentic technical credibility over synthetic AI illustrations.
  2. **Connective Tissue Alignment:** Non-photo visual elements (diagrams, icons) inherit identity kit hex codes (#F8FAFC, #2563EB) for systemic cohesion.
  3. **Discernment Discipline:** Demonstrating engineering maturity means intentionally cutting flashy AI artwork that competes with project evidence.

### 🔹 [Submission 13 — Phase: Foundations & AI Fluency (FL-06 Map Content & CTAs)](submissions/submission_13_content_map.md)
* **What Was Built:** Formulated sharp one-line claim, mapped section-by-section layout with named CTAs leading with FlyRank 88% P@50 case, and compiled honest list of proof assets still to gather.
* **What I Learned:**
  1. **Through-Line Strategy:** Every portfolio section must reinforce the single core claim and point toward the target 15-minute booking CTA.
  2. **Leading with Highest Impact:** Featuring the FlyRank decay prediction model first establishes immediate empirical authority with technical hiring leads.
  3. **Unblocked Build Roadmap:** Cataloging upcoming proof assets (warehouse queries, capstone report PDF) ensures portfolio frontend development stays on schedule.

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
│   ├── submission_06_ml_task_framing.md            <-- Detailed Submission 6 breakdown & learnings
│   ├── submission_07_framed_cases.md               <-- Detailed Submission 7 breakdown & learnings
│   ├── submission_08_prompt_ladder.md               <-- Detailed Submission 8 breakdown & learnings
│   ├── submission_09_prompting_fundamentals.md      <-- Detailed Submission 9 breakdown & learnings
│   ├── submission_10_data_contract.md               <-- Detailed Submission 10 breakdown & learnings
│   ├── submission_11_identity_kit.md                <-- Detailed Submission 11 breakdown & learnings
│   ├── submission_12_curate_images.md                <-- Detailed Submission 12 breakdown & learnings
│   └── submission_13_content_map.md                 <-- Detailed Submission 13 breakdown & learnings
├── notebooks/
│   ├── 01_first_look_and_discovery.ipynb           <-- Executed: Pipeline, discoveries, your turn
│   └── 02_your_first_readable_model.ipynb          <-- Executed: Decision tree, leakage, your turn
└── work/
    └── notebooks/
        ├── w01_research_question.ipynb             <-- Executed: Week 1 framing & live dataset metrics
        ├── w02_ml_task_framing.ipynb               <-- Executed: Week 2 ML task framing & target definition
        └── w03_data_contract.ipynb                 <-- Executed: Week 3 Search Intelligence Data Contract
```
