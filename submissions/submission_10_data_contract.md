# 📑 Submission 10 — Phase: Foundations (ML-04 Search Intelligence Data Contract)

**Notebook Reference:**
* [`work/notebooks/w03_data_contract.ipynb`](../work/notebooks/w03_data_contract.ipynb)

---

## 🎯 1. Assignment Objectives

The primary goals of this Search Intelligence Data Contract assignment were:
1. **Plain-Words Contract (5 Core Answers):** Clearly define unit of analysis (grain), tables used, time window, target proxy, and deliberately excluded fields.
2. **Three Verification Queries:** Prove dataset grain (0 duplicate rows), count row volume & age span, and verify availability filtering with `IS TRUE` (22,006 surviving rows / 73.35%).
3. **5-Feature Frame:** Build a 5-feature dataframe for Lane 2, specifying a one-line "knowable at decision moment because..." justification per feature.
4. **Deliberate Feature Leakage Trap:** Intentionally introduce a target-derived column (`trend_pct`), watch Precision@50 jump to a fake 100.00%, then remove it to preserve honest benchmarks (~77.60%).
5. **Named Slice Limitation:** Document structural limitations regarding historical client depth and static snapshot seasonality.

---

## 🔬 2. Implementation & Data Contract Summary

### A. Plain-Words Contract (Five Core Answers)
1. **Unit of Analysis (Grain):** **One row = One pseudonymized content item (`content_id`)** for a given client site (`client_id`).
2. **Table(s) Used:** `data/raw/content_refresh_anonymized.csv` (and warehouse table `fact_content_daily_performance` for mid-panel month `2026-03`).
3. **Time Window:** Trailing 90-day baseline snapshot with 30-day trailing comparison windows (`impressions_last_30d` vs `impressions_prev_30d`).
4. **Target Proxy Predicted:** Observed relative impression drop proxy $\Delta \text{Imp}_{\text{rel}} = \frac{\text{impressions}_{\text{last 30d}} - \text{impressions}_{\text{prev 30d}}}{\text{impressions}_{\text{prev 30d}} + 1} \times 100$, producing a binary decay flag ($\Delta \text{Imp}_{\text{rel}} < -15.0\%$) to rank top-50 candidates for weekly editorial refresh.
5. **Deliberately Excluded:** `trend_direction` and `trend_pct` (target leakage derived directly from the outcome window) and `health_score` / `is_declining_label` (circular internal product tags).

### B. Three Verification Queries
* **Query 1 (Grain Verification):** Proved zero duplicates returned for `GROUP BY content_id HAVING COUNT(*) > 1` (0 duplicate rows).
* **Query 2 (Row Count & Age Span):** Verified 30,000 raw inventory rows, 22,006 active slice rows (`impressions_90d >= 100`), 30 pseudonymized clients, and content age span (90 to 564 days).
* **Query 3 (Availability Filter with IS TRUE):** Evaluated `(impressions_90d >= 100) == True`, confirming that **22,006 active demand rows (73.35%)** survive filtering.

### C. 5-Feature Frame & Justifications
1. `ctr`: Knowable at decision moment because 90-day historical CTR is recorded in Search Console prior to the prediction window.
2. `avg_position`: Knowable at decision moment because 90-day baseline search ranking position is recorded in Search Console.
3. `content_age_days`: Knowable at decision moment because CMS publication timestamp is fixed at content launch.
4. `days_since_last_update`: Knowable at decision moment because CMS editorial revision logs record the last update timestamp.
5. `engagement_rate`: Knowable at decision moment because GA4 user interaction telemetry is compiled over the 90-day baseline window.

### D. The Feature Leakage Trap Experiment
* **Honest Model (5 Safe Features):** Achieved **77.60% Precision@50** using `GroupKFold` cross-validation on `client_id`.
* **Leaked Model (With `trend_pct`):** Score jumped to **100.00% Precision@50** (fake perfection).
* **Action Taken:** Springing the trap proved why `trend_pct` must be strictly deleted/excluded from model inputs.

### E. Named Slice Limitations
* **Unbalanced Client History & GA4 Tracking Gaps:** Historical depth varies per client (`ga4_data_start`); rows preceding tracking setup have GA4 columns zero-filled with `ga4_data_available = FALSE`.
* **Static Snapshot Seasonality:** A single 90-day snapshot cannot isolate macro seasonal search volume drops without position-adjusted CTR baselines.

---

## 💡 3. What I Learned

1. **Query-Backed Contracts:** Every contract assertion must be verified with an executed query cell rather than assumed.
2. **Availability Filtering Discipline:** Filtering with explicit `IS TRUE` logic ensures non-indexed stub pages do not pollute model training sets.
3. **The Trap Lesson:** Deliberately injecting target leakage demonstrates how trivial it is to get fake 100% scores, reinforcing the necessity of strict feature isolation.
