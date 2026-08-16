# 📑 Submission 14 — Phase: Build (ML-07 Baseline Action Score & Signal Audit)

**Notebook Reference:**
* [`work/notebooks/w04_baseline_score.ipynb`](../work/notebooks/w04_baseline_score.ipynb)

**Generated Metric Receipts:**
* [`work/outputs/baseline_metrics.json`](../work/outputs/baseline_metrics.json)

---

## 🎯 1. Assignment Objectives

The primary goals of this Week 4 Baseline Action Score assignment were:
1. **Signal Audits (2 Signal Checks with Bucket Tables):** Validate two core signals (`days_since_last_update` staleness and `ctr` deficit vs position tier) using printed bucket counts (`n`) and assign one-word verdicts (`CONFIRMED`).
2. **Transparent Rule Encoding:** Formulate one readable heuristic scoring rule using non-fitted weights, assigning a baseline score, reason codes (`CRITICAL_STALE_HIGH_DEMAND`, `STALE_LOW_CTR`), and an action label (`editorial_refresh`).
3. **Ranked Queue CSV Output:** Write the complete sorted queue to `work/outputs/baseline_action_score.csv` from the notebook.
4. **Top-20 Hand Review:** Conduct an item-by-item hand audit of the top 20 ranked candidates, detailing reason code, confidence note, and specific failure triggers ("what would make it wrong").
5. **Weak Pick Analysis & Leakage Assertion:** Identify weak picks flagged by the rule and strictly assert zero target leakage or future-window field usage.

---

## 🔬 2. Implementation & Baseline Performance Summary

### A. Signal Audit Verdicts
1. **Signal 1: Content Staleness (`days_since_last_update`)**
   * **Verdict:** `CONFIRMED`
   * *Evidence:* Bucket table analysis shows decay rate increasing steadily from 62.44% (<90d) up to 80.77% (180–270d stale).
2. **Signal 2: CTR-vs-Position Deficit (`ctr` vs position tier benchmark)**
   * **Verdict:** `CONFIRMED`
   * *Evidence:* Pages with severe CTR deficits (>10% below position tier expectation) experience a 71.03% decay rate compared to 53.32% for pages performing above expected CTR.

### B. Transparent Baseline Rule Formula & Metrics
$$\text{baseline\_score} = \mathbb{I}(\text{days\_since\_update} \ge 90) \times \frac{\text{days\_since\_update}}{30} \times \ln(1 + \text{impressions\_90d}) \times \frac{1}{\text{ctr} + 0.01}$$

* **Active Demand Slice:** 22,006 content pages (`impressions_90d >= 100`)
* **Base Rate (Random Selection):** **64.29%**
* **Baseline Rule Precision@20:** **75.00%**
* **Baseline Rule Precision@50:** **80.00%**
* **Lift over Base Rate:** **1.24x**

### C. Top-20 Hand Review & Weak Picks
* **Top-20 Audit:** Successfully cataloged reason codes, confidence notes, and failure triggers across all 20 highest-ranked content items.
* **Weak Pick 1 (Rank 7 - `content_6476d1d8c050`):** Position 67.8 with 0.00% CTR. Although stale (313d), it resides far beyond page 1-2 search rankings, yielding low editorial ROI.
* **Weak Pick 2 (Rank 8 - `content_4729b57ca036`):** High CTR (3.28%) and strong position (6.8). Despite being 301 days stale, it represents evergreen content (`target_decay_flag = 0`) where forcing an artificial update risks disturbing organic search rank.

### D. Leakage Audit Assertion
* **Prohibited outcome window fields checked:** `impressions_last_30d`, `impressions_prev_30d`, `trend_pct`, `trend_direction` $\rightarrow$ **EXCLUDED**
* **Prohibited product tags checked:** `health_score`, `is_declining_label` $\rightarrow$ **EXCLUDED**
* **Result:** Passed `assert len(leaked_detected) == 0`.

---

## 💡 3. What I Learned

1. **The Power of Readable Baselines:** A simple 3-line heuristic rule achieved **80.00% Precision@50**, setting a transparent benchmark that complex ML models in Week 5 must beat.
2. **Signal Audit Discipline:** Verifying signal strength through bucket tables with printed `n` counts prevents building rules on ungrounded assumptions.
3. **Hand-Review Value:** Auditing top-20 outputs revealed weak picks (e.g. non-indexed stub pages or high-performing evergreen content) that pure summary metrics obscure.
