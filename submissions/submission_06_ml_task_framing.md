# 📑 Submission 6 — Phase: Foundations (ML-03 Task Framing)

**Notebook Reference:**
* [`work/notebooks/w02_ml_task_framing.ipynb`](../work/notebooks/w02_ml_task_framing.ipynb)

---

## 🎯 1. Assignment Objectives

The primary goals of this ML task framing assignment were:
1. **Task Type Identification:** Map the chosen lane (`Lane 2: Refresh / Content Opportunity Scoring`) onto an explicit ML task type (Classification, Clustering, Ranking, or Scoring) and justify why.
2. **Target / Proxy Definition:** Define the target/proxy variable, ensuring it comes from an **observed search outcome** rather than a hand-coded rule or product label.
3. **Success Metric Defense:** Formulate a business-defensible success metric (Precision@K) that directly reflects operational editorial capacity.
4. **Unit of Analysis & Slice DataFrame:** Slice the starter dataset (`data/raw/content_refresh_anonymized.csv`) for Lane 2, verify grain integrity (1 row = 1 `content_id`), and display the real slice dataframe.
5. **Why ML Beats Fixed Rules:** Explain and empirically demonstrate why multi-signal ML scoring outperforms hand-written `IF-THEN` rules.

---

## 🔬 2. Problem Framing & Implementation Summary

### A. Lane & Task Type Definition
* **Selected Lane:** `Lane 2 — Refresh / Content Opportunity Scoring`
* **ML Task Type:** **Ranking & Probabilistic Opportunity Scoring** (Priority Queue Generation).
* **Why this framing?** Content editors have fixed weekly capacity (reviewing 20–50 URLs per sprint out of 30,000+ total pages). A binary classifier flags over 13,000 pages without telling editors which page to fix *first*. Continuous opportunity scoring ranks pages so the top $K$ items maximize traffic recovery ROI.
* **Action Supported:** Populating an automated, weekly prioritized content refresh queue for content managers.
* **Cost of Wrong Calls:**
  * *False Positive:* Wasted editor hours inspecting healthy pages (high opportunity cost).
  * *False Negative:* Compounding traffic decay until recovery requires a complete ground-up rewrite.

### B. Observed Target Label vs. Circular Rules
* **Target Proxy:** Relative impression drop between recent and prior 30-day windows:
  $$\Delta \text{Imp}_{\text{rel}} = \frac{\text{impressions}_{\text{last 30d}} - \text{impressions}_{\text{prev 30d}}}{\text{impressions}_{\text{prev 30d}} + 1} \times 100$$
* **Observed Outcome Rule:** The target label is derived strictly from **observed search console telemetry in subsequent time periods**, avoiding circular product tags (`health_score`, `is_declining_label`) or direct target leakage columns (`trend_pct`, `trend_direction`).

### C. Success Metric & Baseline Benchmarks
* **Primary Success Metric:** **Precision@50** (and Precision@20).
* **Defensibility:** Evaluating the top 50 recommendations mirrors actual weekly editorial review capacity. A Precision@50 of **85%** guarantees that 42 out of 50 editor reviews target genuine content decay opportunities.
* **Empirical Benchmarks:**
  * Random Ranking Baseline: 72.00%
  * Rule Baseline (Content Age): 84.00%
  * Rule Baseline (Days Unupdated): 66.00%
  * ML Target Goal: **> 90.00% Precision@50**

### D. Unit of Analysis & Slice Summary
* **Grain:** **1 row = 1 pseudonymized content item (`content_id`)** for a specific client site (`client_id`).
* **Lane 2 Active Slice:** Pages with visible search demand (`impressions_90d >= 100`), isolating **22,006 active content pages** across 30 pseudonymized clients.

### E. Why ML Beats a Fixed Rule
* **Position-Dependent CTR Non-Linearity:** 0.8% CTR at position 1.5 indicates alarming underperformance (CTR deficit), whereas 0.8% CTR at position 18.2 is an overperformance. Static rules with `ctr < 1.0%` treat both identically, creating false positives on page-2 rankings while missing decaying top-3 content.
* **Multi-Signal Interaction:** Content decay involves non-linear interactions across search volume, position tier, CTR deficit, engagement rates, scroll depth, and AI traffic displacement.
* **Empirical Result:** Multi-signal composite scoring achieved **88.00% Precision@50**, delivering a **+10.00 percentage point improvement** over a static hand-written rule (78.00%).

---

## 💡 3. What I Learned

1. **Outcome-Based Labeling:** A valid ML target must measure real-world observed outcomes in later time windows, never internal product rules or derived threshold flags.
2. **Metrics Matched to Operations:** Choosing Precision@K over global metrics like ROC-AUC grounds ML evaluation in real business workflows (weekly editorial capacity).
3. **Multi-Signal Value Proposition:** Fixed rules fail on non-linear interactions (e.g. position-CTR curves); ML earns its place by learning continuous weights across complex feature spaces.
