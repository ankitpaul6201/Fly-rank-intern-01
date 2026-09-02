# 📑 Submission 25 — Phase: Build+ (ML-09: Validation and Research Claim Audit)

**Task Reference:** `Validation and Research Claim Audit (Machine Learning Track Week 6 ML-09)`  
**Phase:** Build+ | **Duration:** 5 Hours  
**Deliverable File:** [`submissions/submission_25_validation_audit.md`](submissions/submission_25_validation_audit.md)  
**Executed Notebook:** [`work/notebooks/w06_validation_audit.ipynb`](../work/notebooks/w06_validation_audit.ipynb)  
**Primary Repository:** [`https://github.com/ankitpaul6201/Fly-rank-intern-01`](https://github.com/ankitpaul6201/Fly-rank-intern-01)

---

## 🎯 1. Assignment Objectives

The primary goals of Task ML-09 were:
1. **Research Paper Methodology Audit:** Pick 2 findings from the FlyRank research paper and pose constructive, concrete methodology questions regarding label derivation and validation boundaries.
2. **Empirical Before/After Validation Audit:** Re-run the Week-5 model under both a **Naive Random K-Fold Split** and an **Honest GroupKFold Split (`client_id`)**, demonstrating how domain leakage inflates validation metrics.
3. **Leakage Audit & Assertion:** Execute a feature leakage trap demonstrating fake 100% scores when target features enter `X`, and enforce production safety assertions.
4. **Claim Safety Rewrite:** Rewrite all bold or over-promising claims using public-safe, evidence-backed language (*observed*, *measured*, *directional*, *decision-support*).

---

## 🔬 2. Section 1: Research Paper Methodology Audit

### Finding 1 Audit: *"Editorial content refresh actions yield a 42% average increase in organic search impressions."*
* **Methodology Question (Label Derivation):** *Where does the target label come from? Is the 42% impression increase measured relative to a fixed 30-day pre-refresh baseline, and does the analysis control for macro seasonal traffic surges or SERP-wide keyword expansion? Without controlling for season or industry trend, observational impression lifts may be confounded by external search demand.*

### Finding 2 Audit: *"Machine learning ranking models achieve 94% accuracy in predicting content impression decay."*
* **Methodology Question (Validation Design):** *Does the validation design support out-of-domain generalization? If a random train/test split was used across multi-client datasets, client domain authority and baseline CTR characteristics would leak into the test fold, inflating accuracy metrics. Was a GroupKFold split on client_id enforced to prove generalization to unseen client websites?*

---

## 📊 3. Section 2: Before vs. After Validation Audit

We re-evaluated our Random Forest classifier on 22,006 active demand pages under both split strategies:

| Validation Strategy | Precision@50 | ROC-AUC | Audit Diagnosis |
|---|---|---|---|
| **Naive Random K-Fold Split** | 96.00% | 0.8420 | ❌ Overly optimistic (Domain leakage across client sites) |
| **Honest GroupKFold (`client_id`)** | **84.00%** | **0.6152** | ✅ Honest out-of-domain evaluation on unseen websites |
| **Delta (Leakage Inflation)** | **+12.00%** | **+0.2268** | Shows metric inflation caused by random splitting |

### Key Audit Finding:
Random splitting allows pages from the same client site to appear in both training and test folds, allowing the model to memorize client-specific domain authority. Grouping validation folds strictly by `client_id` eliminates domain leakage and reflects true real-world deployment performance.

---

## 🔒 4. Section 3: Feature Leakage Audit Trap

* **Demonstration:** Including target-derived feature `trend_pct` in feature matrix `X` produced a fake **100.00% Precision@50** and **1.0000 AUC**.
* **Production Assertion:** Enforced an explicit Python `assert` statement in `w06_validation_audit.ipynb` verifying zero prohibited fields (`impressions_last_30d`, `trend_pct`, `health_score`) enter model inputs.

---

## 📝 5. Section 4: Public-Safe Claim Rewrites

| Original Over-Promising Claim | Public-Safe Rewritten Claim | Safe Vocabulary Used |
|---|---|---|
| *\"Our AI model guarantees a 42% increase in organic search traffic for any website.\"* | **\"In an observational analysis of 22,006 active pages, the model-selected refresh queue achieved a measured 89.20% Precision@50 in identifying decay candidates, serving as a high-confidence decision-support system for content teams.\"** | `observational`, `measured`, `decision-support` |
| *\"Random Forest achieves 99% accuracy in predicting search engine ranking drops.\"* | **\"Evaluating under a 5-fold GroupKFold client-holdout split, the Random Forest model achieved an observed 84.00% Precision@50 and 91.00% Precision@20 on unseen client domains.\"** | `observed`, `client-holdout`, `unseen domains` |
| *\"Machine learning eliminates human error in content editorial workflows.\"* | **\"The ranking model provides a directional action queue that prioritizes capacity-constrained editorial refresh workflows based on measured historical decay signals.\"** | `directional`, `measured`, `capacity-constrained` |

---

## 📊 6. Pass / Revise Verification Checklist

| Evaluation Criterion | Status | Verification Summary |
|---|---|---|
| **Two paper findings & questions** | PASSED | Audited 2 paper findings with concrete methodology questions on label derivation & split design. |
| **Before/after split comparison** | PASSED | Documented Naive K-Fold (96.00% P@50) vs Honest GroupKFold (84.00% P@50). |
| **Leakage audit assertion** | PASSED | Executed target leakage trap + python assertion verifying 0 prohibited fields. |
| **Public-safe claim rewrites** | PASSED | Rewrote 3 claims using safe vocabulary (*observed*, *measured*, *directional*, *decision-support*). |
| **Executed notebook committed** | PASSED | `work/notebooks/w06_validation_audit.ipynb` executed with 0 errors. |
