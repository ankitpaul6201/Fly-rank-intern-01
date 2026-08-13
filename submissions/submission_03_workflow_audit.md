# 📑 Submission 3 — Setup: AI Workflow Audit & Toolkit Setup (FL-01)

**Task Reference:** `FL-01 — Workflow Audit & Toolkit Setup`  
**Phase:** Setup | **Estimated Hours:** 4  
**Deliverable File:** [`submissions/submission_03_workflow_audit.md`](submissions/submission_03_workflow_audit.md)

---

## 🎯 1. Assignment Objectives

The primary goals of this setup & AI fluency assignment were:
1. **Recurring Task Audit:** Map 12 real, specific weekly tasks across engineering, study, and side projects (e.g. FlyRank ML internship, CP Vault Chrome extension, Campus Buddy).
2. **Task Classification & Rationale:** Classify each task into one of 4 AI interaction modes (*Just Me*, *Delegate with Review*, *Collaborate*, *Fully Automate*) based on Ethan Mollick's task-allocation framework, with a concise one-line rationale.
3. **Toolkit Setup & Verification:** Register free tier accounts for Claude, ChatGPT, and Anthropic Academy, and enroll in *AI Fluency: Framework & Foundations* (completing Module 1).
4. **Claude Project Configuration:** Create a dedicated Claude Project with custom persona, tone preferences, and internship goals.
5. **Target Task Selection (FL-02 to FL-04):** Select 3 specific audit tasks to reuse in upcoming FL modules with measurable "Done Well" success definitions.

---

## 📊 2. Workflow Audit (12 Real Weekly Tasks)

The following table maps my actual weekly engineering, study, and project tasks, evaluated against the AI collaboration spectrum:

| # | Recurring Task | Category / Context | Classification Mode | One-Line Rationale |
|---|---|---|---|---|
| **1** | Solving new Data Structures & Algorithms problems during live competitive programming contests | CP Vault / Study | **Just Me** | Live contests prohibit external assistance, and original algorithmic problem solving builds foundational intuition that AI cannot substitute. |
| **2** | Strategic career planning, internship goal setting, and personal ethics decisions | Personal / FlyRank | **Just Me** | Personal career trajectory, ethical boundaries, and self-reflection require genuine human self-knowledge and personal values. |
| **3** | User empathy & Qualitative UI/UX design decisions for Campus Buddy | Campus Buddy | **Just Me** | Understanding student stress during university shortlisting relies on human qualitative intuition and emotional context that AI lacks. |
| **4** | Writing Python scripts for data cleaning & schema validation on search performance logs | FlyRank ML | **Fully Automate** | Deterministic operations like missing value imputation, data type casting, and range checks are best handled by automated Python scripts. |
| **5** | Generating boilerplate REST API endpoint handlers and service wrappers | Campus Buddy | **Fully Automate** | Creating repetitive CRUD routes following established patterns has high predictability and zero strategic ambiguity. |
| **6** | Parsing & syncing contest submission history in Chrome Extension background scripts | CP Vault | **Delegate to AI with Review** | AI quickly generates Chrome extension async messaging boilerplate, requiring human code review to catch edge cases like storage limits. |
| **7** | Drafting pull request descriptions and technical changelogs | Open Source / FlyRank | **Delegate to AI with Review** | AI synthesizes git diffs into structured summaries efficiently, needing only human verification for technical accuracy before merge. |
| **8** | Writing unit tests for data transformation pipeline utilities (`scripts/ml_utils.py`) | FlyRank ML | **Delegate to AI with Review** | AI excels at expanding edge-case test coverage (`pytest`), while human review ensures assertions test real business requirements. |
| **9** | Designing decision-tree feature selection strategies & avoiding feature leakage | FlyRank ML | **Collaborate with AI** | Interactively testing hypotheses about target leakage with AI combines AI code speed with human domain knowledge about search metrics. |
| **10** | Debugging complex cross-origin background sync errors in browser extensions | CP Vault | **Collaborate with AI** | Pair programming with AI to analyze stack traces speeds up root-cause diagnosis while human tests verify fixes in live browser state. |
| **11** | Summarizing ML research papers on content decay and search ranking algorithms | Study / Research | **Collaborate with AI** | AI extracts key methodology points rapidly, while human critical thinking evaluates applicability to FlyRank's 30k page dataset. |
| **12** | Writing custom SQL queries for multi-client aggregation in DuckDB / BigQuery | FlyRank ML | **Collaborate with AI** | AI assists with complex window functions and CTEs, while human inspection verifies join correctness and client holdout integrity. |

---

## 🛠️ 3. Toolkit Setup & Account Verification

### A. Registered Free Toolkit
- **Anthropic Claude Account:** Active (Free Tier)
- **OpenAI ChatGPT Account:** Active (Free Tier)
- **Anthropic Academy Account:** Registered & Enrolled in *AI Fluency: Framework & Foundations*

### B. Module Completion & Verification Evidence
- **Course Title:** *AI Fluency: Framework & Foundations* (Anthropic Academy)
- **Progress:** Module 1 ("Foundations of AI Collaboration & Ethical Usage") completed.
- **Evidence Screenshots:**
  - *Academy Enrollment & Progress:*  
    `![Anthropic Academy Enrollment](../outputs/screenshots/anthropic_academy_enrollment.png)`  
    *(Verification screenshot showing active enrollment and Module 1 completion badge)*
  - *Claude & ChatGPT Accounts:*  
    `![Claude and ChatGPT Setup](../outputs/screenshots/claude_chatgpt_account_setup.png)`  
    *(Verification screenshot showing active account dashboard)*

---

## ⚙️ 4. Claude Project Configuration

Created a custom **Claude Project** named `FlyRank-ML-Internship` with tailored system instructions to align AI responses with internship priorities.

### A. Configured Custom Instructions
```text
WHO I AM:
I am an ML & Full-Stack Software Engineering Intern at FlyRank. I work on search performance decay prediction, building readable ML decision models (pandas, scikit-learn, DuckDB), and developing full-stack web applications (React, Node.js, Chrome Extensions).

TONE & STYLE PREFERENCES:
- Concise, technical, direct, and pragmatic.
- Prioritize clean, production-grade code snippets with minimal conversational filler.
- Format complex explanations using markdown tables, bullet points, and explicit code diffs.
- Always highlight edge cases, memory/compute constraints, and potential data leakage risks.

CURRENT GOALS:
1. Master applied ML decision support systems on search analytics datasets (30,000+ rows).
2. Build scalable feature pipelines while maintaining strict feature leakage discipline.
3. Develop peak AI fluency by systematically knowing when to delegate, collaborate, automate, or keep tasks strictly manual.
```

### B. Configuration Evidence Screenshot
`![Claude Project Custom Instructions](../outputs/screenshots/claude_project_config.png)`  
*(Screenshot showing configured Project Instructions in Claude interface)*

---

## 🎯 5. Three Target Tasks for FL-02 through FL-04 & Success Definitions

The three specific tasks selected for deep-dive optimization in FL-02, FL-03, and FL-04 are detailed below with explicit, measurable "Done Well" criteria:

### 📍 Target Task 1: Automated SEO Content Decay Feature Engineering & SQL Query Generation (FL-02 Target)
* **Mode:** `Collaborate with AI`
* **Context:** Building DuckDB / Pandas feature extraction logic to turn raw page impression and position histories into multi-horizon trend signals for model training.
* **"Done Well" Success Definition (Measurable):**
  1. Feature extraction code produces 10+ decay indicators (e.g. `ctr_decay_30d`, `position_velocity`, `impression_volatility`) without throwing syntax or execution errors.
  2. Zero target leakage: All generated features strictly use historical pre-decision window data (verified via dataset audit).
  3. Execution efficiency: Query / script executes over the 30,000-row dataset in $< 10$ seconds on local CPU.
  4. Code cleanliness: Fully typed pandas / SQL code with inline docstrings explaining mathematical logic.

### 📍 Target Task 2: Drafting Technical Architecture Summaries & Pull Request Documentation (FL-03 Target)
* **Mode:** `Delegate to AI with Review`
* **Context:** Synthesizing complex PR diffs, model evaluation results (e.g. Precision@50 lift over baseline), and data boundary assumptions into clear technical documentation for team review.
* **"Done Well" Success Definition (Measurable):**
  1. Complete PR template coverage: Automatically generates context, architectural diff, risk analysis, and testing steps from `git diff`.
  2. Review efficiency: Requires $< 2$ minor edits during human review before being merge-ready.
  3. Clarity & Precision: Accurately states model evaluation metrics (e.g., Precision@50 = 0.740 vs Baseline 0.240) and explicitly states epistemic claim boundaries (observational vs causal).
  4. Time savings: Reduces documentation drafting time from 25 minutes down to $< 5$ minutes per submission.

### 📍 Target Task 3: Data Cleaning & Schema Validation Pipeline for Search Logs (FL-04 Target)
* **Mode:** `Fully Automate`
* **Context:** Running deterministic pre-processing routines on incoming pseudonymized CSV logs to handle missing values, validate numeric boundaries, and format data types.
* **"Done Well" Success Definition (Measurable):**
  1. 100% Schema Compliance: Automatically detects and handles missing values, invalid data types, and out-of-bound values (e.g. CTR $> 1.0$ or negative impressions) without manual intervention.
  2. Zero Pipeline Crashes: Script runs headlessly in CI/CD pipeline (`smoke-test.yml`) with exit code 0 across 100% of test batches.
  3. Audit Log Generation: Outputs structured JSON summary report logging total rows processed, null counts, and imputed values.
  4. Speed: Processes 30,000 rows in $< 3$ seconds.

---

## 💡 6. What I Learned

### Key Mastery Takeaways:
1. **The Spectrum of AI Fluency:**
   * AI fluency is not using AI for everything. It is knowing precisely when AI accelerates work (collaborating on SQL/feature logic), when AI handles repetitive drafting (delegating PR notes with human review), when code handles work deterministically (fully automating data validation), and when human intuition is mandatory (just me for contest algorithms and UX empathy).
2. **Ethan Mollick's Allocation Principles:**
   * High-value tasks require human oversight. Delegating without review leads to subtle bugs (e.g. target leakage in ML features), whereas keeping deterministic tasks manual wastes human cognitive bandwidth.
3. **Contextualizing AI Tools via Projects:**
   * Setting explicit Claude Project instructions (role, tone, strict constraints) eliminates back-and-forth prompt tuning and ensures AI outputs immediately match production standards.

---
