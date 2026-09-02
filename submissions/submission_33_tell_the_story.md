# 📑 Submission 33 — Phase: Submit (ML-12: Tell the Story)

**Task Reference:** `Tell the Story (Machine Learning Track Week 8 ML-12)`  
**Phase:** Submit / Storytelling | **Duration:** 2 Hours  
**Deliverable File:** [`submissions/submission_33_tell_the_story.md`](submissions/submission_33_tell_the_story.md)  
**Live Deployed Research Paper URL:** [`https://flyrank.ankitpaul.me/`](https://flyrank.ankitpaul.me/)  
**Executed Notebook:** [`work/notebooks/capstone.ipynb`](../work/notebooks/capstone.ipynb)  
**Exported Figure:** [`work/figures/capstone_model_vs_baseline.png`](../work/figures/capstone_model_vs_baseline.png)  
**Primary Repository:** [`https://github.com/ankitpaul6201/Fly-rank-intern-01`](https://github.com/ankitpaul6201/Fly-rank-intern-01)

---

## 🎯 1. Assignment Objectives & Storytelling Scope

Task ML-12 translates our technical capstone research paper into three distinct audience-specific narratives:
1. **Case Study Framing inside Live Paper:** Abstract and Introduction tie findings directly to the real FlyRank content refresh problem in public-safe language.
2. **5-Minute Showcase Demo Outline:** Closing section in `work/notebooks/capstone.ipynb` structured for live technical presentation (Question → Method → 1 Chart → 1 Honest Result → 1 Recommendation).
3. **Two Shareable Story Cuts:** Formatted social post (Cut A) and employer-facing 3-sentence summary (Cut B) committed directly in `work/notebooks/capstone.ipynb`.

---

## ⏱️ 2. 5-Minute Technical Showcase Demo Outline

*(Committed as Section 8 in `work/notebooks/capstone.ipynb`)*

* **0:00 - 1:00 (The Problem & Research Question):**  
  How do digital publishing teams catch organic search traffic decay before impression drops occur? We introduce the **Lane 2 Content Refresh Opportunity Scoring Engine** trained on 79M anonymized search queries.
* **1:00 - 2:00 (The Methodology & Validation Split):**  
  Filtered 22,006 active demand pages (`impressions_90d >= 100`). Built safe pre-decay feature matrix (`ctr`, `avg_position`, `content_age_days`, `days_since_last_update`, `engagement_rate`). Applied strict 5-fold `GroupKFold` split grouped by `client_id` to evaluate true out-of-domain generalization.
* **2:00 - 3:00 (The Key Performance Chart):**  
  Showcase `work/figures/capstone_model_vs_baseline.png`. Logistic Regression model achieves **84.00% Precision@50** and **91.00% Precision@20** vs **42.00% heuristic baseline**.
* **3:00 - 4:00 (The Honest Result & Leakage Warning):**  
  Demonstrate how naive random splitting leaks client domain authority to fake 96.00% P@50 scores. Explain why `GroupKFold` client holdout is mandatory for honest evaluation.
* **4:00 - 5:00 (Action Playbook & Operational Impact):**  
  Map predictions to 5 transparent reason codes (`CRITICAL_STALE_HIGH_DEMAND`, `STALE_LOW_CTR`, etc.) with strict human review guardrails.

---

## 📢 3. Two Shareable Story Cuts

*(Committed as Section 9 in `work/notebooks/capstone.ipynb`)*

### 🔹 Cut A: Technical Social Media Post (LinkedIn / X)
> Most ML models look great in Jupyter notebooks until they hit real-world production. While evaluating a search traffic decay prediction model on 79M search queries, a naive 80/20 random split gave an impressive 96% Precision@50. But because pages from the same client domain appeared in both train and test folds, the model was memorizing client authority rather than learning generalizable decay signals.
>
> By switching to a `GroupKFold` split grouped by `client_id`, we eliminated domain leakage and established an honest **84.00% Precision@50** out-of-domain baseline (2x higher than static content-age rules).
>
> Read the full live research paper & interactive playbook: https://flyrank.ankitpaul.me/

---

### 🔹 Cut B: Employer-Facing 3-Sentence Summary
> I built a Content Refresh Opportunity Scoring Engine that predicts organic search traffic decay on a 22,006-page slice of 79 million anonymized search queries. Using a 5-fold GroupKFold cross-validation split grouped by client ID to prevent domain leakage, the Logistic Regression model achieved an 84.00% Precision@50 and 91.00% Precision@20, doubling the performance of traditional content-age rules. I translated these predictions into an operational, human-reviewed Content Action Playbook with transparent reason codes and strict no-go automation guardrails: https://flyrank.ankitpaul.me/

---

## 📊 4. Pass / Revise Verification Checklist

| Evaluation Criterion | Status | Verification Summary |
|---|---|---|
| **Case Study Paper Framing** | PASSED | Abstract & Intro tie findings directly to real FlyRank content refresh problem. |
| **5-Minute Showcase Outline** | PASSED | Added 5-minute showcase outline in Section 8 of `capstone.ipynb`. |
| **Two Shareable Story Cuts** | PASSED | Added Technical Social Post & 3-Sentence Employer Summary in Section 9 of `capstone.ipynb`. |
| **Live Deployed Paper** | PASSED | Live over HTTPS at [https://flyrank.ankitpaul.me/](https://flyrank.ankitpaul.me/). |
| **Committed Repository Work** | PASSED | `work/notebooks/capstone.ipynb` executed and pushed cleanly to `main`. |
