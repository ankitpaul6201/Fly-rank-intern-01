# 📌 FlyRank ML Internship — Submissions Overview

Welcome to the **Submission Overview** for this repository. This document explains everything accomplished across each track assignment in simple, easy-to-understand terms—from initial setup and starter experiments to ML model evaluation and research question framing.

---

## 🚀 Overview of Submissions Completed

| # | Assignment / Phase | Status | Key Notebook / File | Simple Summary |
|---|---|---|---|---|
| **1** | **Phase: Setup (Week 1 & 2 Starter Notebooks)** | ✅ Completed & Executed | [`notebooks/01_first_look_and_discovery.ipynb`](notebooks/01_first_look_and_discovery.ipynb)<br>[`notebooks/02_your_first_readable_model.ipynb`](notebooks/02_your_first_readable_model.ipynb) | Ran the baseline ML pipeline, compared hand-written rules vs. machine learning models, discovered data truths, and learned feature leakage protection. |
| **2** | **Week 1: Research Question & Problem Framing** | ✅ Completed & Executed | [`work/notebooks/w01_research_question.ipynb`](work/notebooks/w01_research_question.ipynb) | Selected **Lane 2: Refresh Opportunity Scoring**, defined the decision/action framework, backed choices with 3 live dataset numbers, and set claim boundaries. |

---

## 📑 Submission 1 Details: Setup & Starter Notebooks

### 🎯 Objective
Run a real Machine Learning pipeline on 30,000 anonymized search data rows to watch a learned model beat a hand-written rule, discover data insights using Pandas, and build readable decision trees.

### 🔍 Key Findings & Notebook Highlights

#### 1. Notebook 01 — [`notebooks/01_first_look_and_discovery.ipynb`](notebooks/01_first_look_and_discovery.ipynb)
* **Hand-Written Rule vs. Machine Learning:**
  * **Hand-Written Rule (Precision@50):** `0.240` (~12 of top 50 correct).
  * **Random Forest Model (Precision@50):** `0.740` (~37 of top 50 correct).
  * **Takeaway:** The learned ML model beat the fixed rule by roughly **3x**.
* **Discovery A (Search Volume vs. Actual Traffic):**
  * Filtered pages with active impressions (`impressions_90d > 0`).
  * Discovered that keyword search volume correlates weakly with actual impressions received. High search volume does not guarantee high traffic.
* **Discovery B (CTR Cliff & Content Types):**
  * Click-through rate (CTR) drops steeply as ranking position worsens.
  * Identified which content types experience the lowest CTR within position tiers.
* **Discovery C (Content Length vs. Trend Direction):**
  * Median word count between declining (`down`) and growing (`up`) pages is nearly identical (~1,200 words), proving that content length alone does not prevent traffic decay.

#### 2. Notebook 02 — [`notebooks/02_your_first_readable_model.ipynb`](notebooks/02_your_first_readable_model.ipynb)
* **Readable Decision Trees:**
  * Trained depth-2, depth-3, and depth-4 Decision Trees to inspect explicit `if/else` decision rules (e.g., splitting on `days_since_last_update` and `impressions_90d`).
* **Feature Variations:**
  * Tested swapping features (e.g. replacing `impressions_90d` with `engagement_rate`).
* **Feature Leakage Lesson:**
  * Demonstrated why outcome-derived signals (like `trend_pct`) must never be used as inputs. Feeding the target in disguise gives fake 100% performance without learning real signals.
* **Client-Holdout Validation:**
  * Evaluated model performance using `GroupShuffleSplit` on `client_id` so pages from the same client never appear in both training and test sets.

---

## 📑 Submission 2 Details: Research Question & Lane Framing

### 🎯 Objective
Frame a real-world machine learning problem by picking a project lane, defining who uses the model, identifying the cost of wrong decisions, and backing the selection with live data evidence.

### 📌 Selected Lane: `Lane 2 — Refresh / Content Opportunity Scoring`
* **Why Lane 2?** Websites have thousands of pages, but content marketing teams have limited weekly hours. Lane 2 automatically ranks declining pages that need updates, expansion, or protection so reviewers spend time on high-impact pages first.

### 💡 Problem Framing Summary
* **Research Question:** *"How can we prioritize declining and decay-risk content pages for review so content teams maximize traffic preservation per editorial hour spent?"*
* **Unit of Analysis (Grain):** A single content page (`content_id`).
* **Decision Improved:** Which top 20–50 candidate pages an editorial team should review and refresh during their weekly sprint.
* **Concrete Action:** Updating stale facts, expanding thin content, updating meta descriptions, or re-aligning search intent.
* **Cost of Wrong Calls:**
  * *False Positive (Flagging a healthy page):* Wasted editorial hours spent auditing pages that didn't need intervention.
  * *False Negative (Missing a decaying page):* Unnoticed traffic decay compounding over months until recovery requires a full rewrite.

### 📊 Live Dataset Proof (30,000 Anonymized Pages)
* **Total Dataset Size:** 30,000 anonymized pages.
* **Overall Decline Rate:** **16,262 pages (54.21%)** show a downward traffic trend (`trend_direction == 'down'`).
* **Active Demand Pages:** **22,006 pages (73.35%)** receive active demand (`impressions_90d >= 100`).
* **Visible Declining Pages:** **13,152 pages (59.77% of visible demand)** are actively declining—creating a massive backlog that requires automated ML prioritization.

### 🛡️ Claim Boundaries (Careful Language)
* **What we CAN claim:** Observational correlations, probabilistic ranking, and decision-support guidance.
* **What we CANNOT claim:** Causal proof (we cannot guarantee a refresh *causes* recovery without A/B testing) or reverse-engineering search algorithms.

---

## 🛠️ Repository File Map

```text
flyrank-ml-internship-starter/
├── SUBMISSION_OVERVIEW.md                 <-- You are here (Summary of all deliverables)
├── README.md                              <-- Starter overview & Colab badges
├── SETUP.md                               <-- Setup instructions & Hugging Face access guide
├── GUIDE.md                               <-- Map of files, rules, and architecture
├── notebooks/
│   ├── 01_first_look_and_discovery.ipynb  <-- Executed: Pipeline, discoveries A/B/C, your turn
│   └── 02_your_first_readable_model.ipynb <-- Executed: Decision tree, feature leakage, your turn
└── work/
    └── notebooks/
        └── w01_research_question.ipynb    <-- Executed: Week 1 framing & live dataset metrics
```
