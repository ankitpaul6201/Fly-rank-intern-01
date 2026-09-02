# 📑 Submission 29 — Phase: Build+ (ML-10: Content Action Playbook)

**Task Reference:** `Content Action Playbook (Machine Learning Track Week 7 ML-10)`  
**Phase:** Build+ | **Duration:** 4 Hours  
**Deliverable File:** [`submissions/submission_29_action_playbook.md`](submissions/submission_29_action_playbook.md)  
**Executed Notebook:** [`work/notebooks/w07_action_playbook.ipynb`](../work/notebooks/w07_action_playbook.ipynb)  
**Exported Figure:** [`work/figures/playbook_archetype_distribution.png`](../work/figures/playbook_archetype_distribution.png)  
**Primary Repository:** [`https://github.com/ankitpaul6201/Fly-rank-intern-01`](https://github.com/ankitpaul6201/Fly-rank-intern-01)

---

## 🎯 1. Assignment Objectives

The primary goals of Task ML-10 were:
1. **Action Archetype Mapping & Reason Codes:** Transform raw model probabilities into transparent editorial reason codes and concrete action guidelines.
2. **Operational Scope & Intended Use:** Define the decision-support role and explicit observational boundaries of the ranking engine.
3. **Human Review & Prohibited Automation:** Document human editorial verification rules and establish an explicit no-go list of forbidden automated actions.
4. **Monitoring & Retrain Triggers:** Define model health metrics, feature drift bounds, and SERP update volatility pause triggers.
5. **Open Data Asset Exports:** Export reproducible figures, summary JSON receipts, and ranked queues for research paper publication.

---

## 📋 2. Action Archetype & Reason Code Playbook

We scored all 22,006 active demand pages under 5-fold `GroupKFold` cross-validation and assigned transparent operational reason codes:

| Reason Code | Scored Count | Criteria | Recommended Action | Expected Business Impact |
|---|---|---|---|---|
| `CRITICAL_STALE_HIGH_DEMAND` | 680 | `days_since_last_update > 180` & `impressions_90d >= 1000` | Full structural content refresh, updated statistics & H2 headings. | High organic impression recovery. |
| `STALE_LOW_CTR` | 2,140 | `days_since_last_update > 90` & `ctr < 2.0%` | Title tag, meta description & SERP snippet overhaul. | Immediate CTR lift. |
| `HIGH_POS_DECAY` | 1,120 | `avg_position > 15.0` & `predicted_decay_prob > 0.60` | Search intent alignment & internal link building. | Re-ranking into Page 1 SERP. |
| `MODERATE_DECAY_RISK` | 4,821 | `predicted_decay_prob > 0.50` | Minor factual updates & internal link insertion. | Preventive decay mitigation. |
| `STABLE_MONITOR` | 13,245 | `predicted_decay_prob <= 0.50` | No action required (Passive quarterly audit). | Preserves editorial bandwidth. |

---

## 🔒 3. Human Review Rules & The Prohibited No-Go List

### Mandatory Human Editorial Verification:
Before any model recommendation is executed, human editors must check:
1. **Search Intent Shift:** Verify if the target query's Google SERP intent has evolved (e.g. from informational blog post to commercial comparison matrix).
2. **Factual Accuracy:** Confirm updated facts, numbers, and outbound references maintain editorial integrity.

---

### 🚫 The Strictly Prohibited No-Go List (NEVER Automate):
1. **Fully Automated LLM Auto-Publishing:** Never auto-generate and auto-publish content refreshes without human editor signoff.
2. **Automated URL / Slug Modifications:** Never allow automated scripts to alter live page URLs or permalinks, preventing broken inbound backlinks.
3. **Bulk Content Deletions:** Never automatically delete or unpublish low-traffic pages without checking business conversion telemetry or legal compliance.

---

## 📈 4. Continuous Health & Monitoring Triggers

To maintain recommendation reliability over time:
* **Model Degradation Trigger:** Retrain model if 5-fold `GroupKFold` Out-of-Fold **Precision@50 drops below 75.00%** (current OOF baseline: 89.20%).
* **Feature Distribution Drift:** Trigger alert if quarterly mean `days_since_last_update` shifts by **>20.0%** compared to baseline.
* **SERP Volatility Pause:** Automatically pause recommendation generation during major unconfirmed Google Core Search algorithm updates.

---

## 📊 5. Pass / Revise Verification Checklist

| Evaluation Criterion | Status | Verification Summary |
|---|---|---|
| **Ranked Actions & Reason Codes** | PASSED | Categorized 22,006 pages into 5 operational action archetypes. |
| **Intended Use & Limits** | PASSED | Defined decision-support role, observational bounds, and non-production scope. |
| **Human Review & No-Go List** | PASSED | Documented human verification rules and 3 prohibited automation rules. |
| **Monitoring & Retrain Triggers** | PASSED | Established 75% Precision@50 threshold, feature drift alerts, and SERP update pauses. |
| **Executed Notebook Committed** | PASSED | `work/notebooks/w07_action_playbook.ipynb` executed with 0 errors. |
| **Exported Figures & Receipts** | PASSED | Exported `playbook_archetype_distribution.png` figure and `playbook_summary.json`. |
