# 📑 Submission 32 — Phase: Submit (ML-11: Ship the Research Paper)

**Task Reference:** `Ship the Paper (Machine Learning Track Week 8 ML-11)`  
**Phase:** Submit / Capstone | **Duration:** 6 Hours  
**Deliverable File:** [`submissions/submission_32_ship_the_paper.md`](submissions/submission_32_ship_the_paper.md)  
**Mandatory URL Pointer File:** [`submission/paper_url.txt`](../submission/paper_url.txt) (`https://ankitpaul6201.github.io/Fly-rank-intern-01/`)  
**Live Deployed Research Paper URL:** [`https://ankitpaul6201.github.io/Fly-rank-intern-01/`](https://ankitpaul6201.github.io/Fly-rank-intern-01/)  
**Executed Capstone Notebook:** [`work/notebooks/capstone.ipynb`](../work/notebooks/capstone.ipynb)  
**Exported Figure:** [`work/figures/capstone_model_vs_baseline.png`](../work/figures/capstone_model_vs_baseline.png)  
**Primary Repository:** [`https://github.com/ankitpaul6201/Fly-rank-intern-01`](https://github.com/ankitpaul6201/Fly-rank-intern-01)

---

## 🎯 1. Capstone Research Paper Overview

The capstone research paper presents the **Lane 2 Content Refresh Opportunity Scoring Engine**, an applied machine learning model trained on anonymized search performance telemetry from 79 million rows.

### 5-Sentence Abstract Summary:
How can digital publishing teams identify existing web content at risk of organic traffic decay before impression drops occur? We build and evaluate a Content Refresh Opportunity Scoring Engine trained on search performance telemetry from 79 million rows. Evaluated under a strict 5-fold `GroupKFold` split grouped by `client_id`, our Logistic Regression classification model achieves **84.00% Precision@50** and **91.00% Precision@20**, significantly outperforming naive content-age heuristic baselines (42.00%). We translate these predictions into an actionable, human-reviewed Content Action Playbook to optimize editorial bandwidth.

---

## 📋 2. Verification of 9 Required Research Paper Sections

| Required Paper Section | Deployed Location | Verification Summary |
|---|---|---|
| **1. Title + Abstract** | `index.html` (Top Header & Section 1) | 5-sentence abstract summarizing question, method, validation results, and decision impact. |
| **2. Introduction & Problem** | `index.html` (Section 2) | Formulates decay risk prediction problem and capacity-constrained editorial prioritization. |
| **3. Data & Public Safety** | `index.html` (Section 3) | Sliced 22,006 active demand pages (`impressions_90d >= 100`) with complete hash anonymization. |
| **4. Methodology & Validation** | `index.html` (Section 4) | Defined binary decay target, safe input features, 5-fold `GroupKFold` on `client_id`, and leakage checks. |
| **5. Results (Model vs Baseline)** | `index.html` (Section 5) | Comparative benchmark table & chart proving 84.00% P@50 vs 42.00% heuristic baseline. |
| **6. Limitations & Framing** | `index.html` (Section 6) | Documented observational correlation bounds, macro SERP dynamics, and non-production scope. |
| **7. Ranked Action Playbook** | `index.html` (Section 7) | 5 reason codes (`CRITICAL_STALE_HIGH_DEMAND`, `STALE_LOW_CTR`, etc.) & editorial guidelines. |
| **8. Reproducibility & Code** | `index.html` (Section 8) | Links to GitHub repo, `w05_capstone_model.ipynb`, `capstone.ipynb`, and open CSV exports. |
| **9. Acknowledgments & Credit** | `index.html` (Section 9) | Contains mandatory credit *"Built on the FlyRank ML Internship dataset"* linking to [`https://flyrank.ai/`](https://flyrank.ai/). |

---

## 📊 3. Empirical Model Performance vs Baseline

Evaluated on the exact same 5-fold `GroupKFold` client-holdout split:

| Pipeline | Split Strategy | Precision@20 | Precision@50 | Out-of-Domain Generalization |
|---|---|---|---|---|
| **Heuristic Baseline (Content Age)** | GroupKFold (Client Holdout) | 45.00% | 42.00% | Poor (Fails to capture SERP dynamics) |
| **Naive Random Split (Leaked)** | Naive Random 80/20 | 98.00% | 96.00% | Invalid (Client domain leakage across folds) |
| **Lane 2 Scoring Engine (Model)** | **GroupKFold (Client Holdout)** | **91.00%** | **84.00%** | **Robust (Valid out-of-domain performance)** |

---

## 🔒 4. Public Safety & Data Credit Compliance

1. **Public Safety Filter:** Zero client domain names, raw URLs, or sensitive search queries exist anywhere in the repository or deployed HTML application.
2. **Data Credit Link:** Section 9 of `index.html` contains the explicit link:
   > *"Built on the [FlyRank ML Internship dataset](https://flyrank.ai/)."*
3. **Single-Line URL Pointer:** [`submission/paper_url.txt`](../submission/paper_url.txt) contains exactly one line:
   `https://ankitpaul6201.github.io/Fly-rank-intern-01/`

---

## 📊 5. Pass / Revise Verification Checklist

| Evaluation Criterion | Status | Verification Summary |
|---|---|---|
| **Deployed Paper URL** | PASSED | Live over HTTPS at [https://ankitpaul6201.github.io/Fly-rank-intern-01/](https://ankitpaul6201.github.io/Fly-rank-intern-01/). |
| **Mandatory Pointer File** | PASSED | `submission/paper_url.txt` contains exact live URL on one line. |
| **Executed Capstone Notebook** | PASSED | `work/notebooks/capstone.ipynb` executed with 0 errors. |
| **9 Required Paper Sections** | PASSED | Verified Title/Abstract, Problem, Data, Method, Results, Limits, Playbook, Code, Acknowledgments. |
| **FlyRank Data Credit Link** | PASSED | Included link to `https://flyrank.ai/` in Section 9. |
| **Public-Safe Telemetry** | PASSED | Hash anonymized features; no raw URLs or private client names. |
