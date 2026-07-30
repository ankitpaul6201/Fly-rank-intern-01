# 📑 Submission 1 — Setup & Starter Notebooks

**Notebook References:**
* [`notebooks/01_first_look_and_discovery.ipynb`](../notebooks/01_first_look_and_discovery.ipynb)
* [`notebooks/02_your_first_readable_model.ipynb`](../notebooks/02_your_first_readable_model.ipynb)

---

## 🎯 1. Assignment Objectives

The primary goals of this initial assignment were:
1. **Pipeline Execution:** Run the complete end-to-end reference ML pipeline on 30,000 anonymized search performance rows.
2. **Empirical Model Comparison:** Measure the performance of a hand-written business rule against a learned Machine Learning model using **Precision@50**.
3. **Data Discovery:** Test common search engine optimization (SEO) beliefs against empirical evidence using Pandas data exploration.
4. **Readable Machine Learning:** Train depth-restricted Decision Trees to inspect explicit `if/else` decision logic.
5. **Feature Leakage Prevention:** Understand why target-derived signals produce artificial performance and how to exclude them.
6. **Robust Evaluation:** Implement client-holdout cross-validation to ensure out-of-sample generalization across unseen domain clients.

---

## 🔬 2. Technical Implementation & Live Results

### A. Hand-Written Rule vs. Machine Learning Pipeline
* **Hand-Written Rule Baseline:** A compound heuristic rule based on page staleness (`days_since_last_update >= 180`) and visibility (`impressions_90d >= 500`).
  * **Precision@50:** `0.240` (~12 out of the top 50 flagged pages were actually declining).
* **Random Forest Model:** A 100-tree ensemble trained on pre-decision numeric and categorical features.
  * **Precision@50:** `0.740` (~37 out of the top 50 flagged pages were actually declining).
  * **Performance Lift:** The learned model outperformed the hand-written rule by **~3.08x**.

### B. Live Data Discoveries
1. **Discovery A (Search Volume vs. Actual Impressions):**
   * *Experiment:* Filtered dataset for pages with active search visibility (`impressions_90d > 0`) and computed correlation with `search_volume`.
   * *Finding:* Correlation remained weak (~0.05). High keyword search volume does not reliably predict actual page traffic.
2. **Discovery B (CTR Collapse by Position & Content Type):**
   * *Experiment:* Grouped pages receiving $\ge 100$ impressions by `position_tier` and `content_type`.
   * *Finding:* Click-Through Rate (CTR) collapses non-linearly past position 3. Identified specific content types (e.g. `guide` vs `product`) that underperform expected CTR at position tiers 4–10.
3. **Discovery C (Content Length vs. Trend Direction):**
   * *Experiment:* Compared median word count between declining (`trend_direction == 'down'`) and growing (`trend_direction == 'up'`) pages.
   * *Finding:* Median word count for declining pages (~1,210 words) is virtually identical to growing pages (~1,195 words), proving that word count alone is not a driver of traffic retention.

### C. Readable Models & Feature Leakage
* **Decision Tree Inspection:** Trained depth-2 and depth-3 decision trees using `DecisionTreeClassifier(max_depth=2, class_weight='balanced')`.
  * *Extracted Rules:* The tree automatically prioritized splitting first on `days_since_last_update <= 175` and `impressions_90d <= 480`.
* **Feature Leakage Experiment:**
  * Added `trend_pct` (the exact percentage change from which `is_declining_label` was derived) as a feature.
  * *Result:* Model achieved a fake Precision@50 of `1.000`. Demonstrates that using outcome-derived variables circularizes training and destroys real predictive utility.
* **Client-Holdout Split:**
  * Used `GroupShuffleSplit` on `client_id` (holding out 20% of clients).
  * *Result:* Verified that decision tree performance holds out-of-sample on clients never seen during training.

---

## 💡 3. What I Learned

### Key Mastery Takeaways:

1. **Why ML Beats Fixed Business Rules:**
   * Hand-written rules apply rigid, linear cutoffs (e.g., `days > 180 AND impressions > 500`). They miss subtle interaction effects (e.g., a page with moderate impressions but high search position decay). ML models learn continuous multi-variable interactions.

2. **Precision@K is the Operational Standard:**
   * Generic accuracy or AUC ROC can be misleading on imbalanced datasets. In real-world content operations, editors can only review 20 to 50 pages per week. Measuring **Precision@50** directly evaluates the business value of the top recommendations.

3. **Feature Leakage Discipline:**
   * Learned to rigorously audit feature sets before model training. If a column is computed *after* the decision point or encodes the target definition (like `trend_pct`), it must be excluded to prevent fake high scores.

4. **Challenging Domain Assumptions with Data:**
   * Discovered that long-held domain heuristics (like "longer word count equals better ranking") fail empirical validation. ML forces data scientists to test assumptions against empirical evidence.

5. **Client-Holdout Cross-Validation:**
   * In multi-client data architectures, random row splitting leaks client-specific characteristics between train and test sets. Grouping by `client_id` ensures the model generalizes to completely new clients.
