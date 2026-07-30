# 📑 Submission 2 — Week 1 Research Question & Problem Framing

**Notebook Reference:**
* [`work/notebooks/w01_research_question.ipynb`](../work/notebooks/w01_research_question.ipynb)

---

## 🎯 1. Assignment Objectives

The primary goals of this problem-framing assignment were:
1. **Lane Selection:** Select a core project direction from the repository lane guide (`docs/ml-intern-dataset-and-lane-guide.md`).
2. **Problem Framing:** Define the concrete human decision, unit of analysis (grain), recommended action, and cost of wrong calls.
3. **Empirical Justification:** Extract live statistics from the 30,000-row starter dataset (`data/raw/content_refresh_anonymized.csv`) to prove the lane is worth pursuing.
4. **Claim Boundaries:** Establish clear epistemic boundaries separating what observational data can prove from what it cannot.

---

## 🔬 2. Problem Framing & Live Data Analysis

### A. Selected Lane & Operational Rationale
* **Selected Lane:** `Lane 2 — Refresh / Content Opportunity Scoring`
* **Why Lane 2?** Mature websites accumulate thousands of content pages over time. Because editorial resources are strictly capacity-constrained, manual review of the entire inventory is impossible. Lane 2 creates an automated, evidence-backed queue of pages to refresh before traffic drops become permanent.

### B. The Decision-Action Framework
* **Research Question:** *"How can we prioritize declining and decay-risk content pages for review so content teams maximize traffic preservation per editorial hour spent?"*
* **Unit of Analysis (Grain):** A single pseudonymized content page (`content_id`).
* **Decision Improved:** Selecting the top 20–50 candidate pages for the editorial team's weekly refresh sprint.
* **Concrete Action:** Initiating targeted content updates (refreshing outdated stats, expanding thin sections, updating meta descriptions, or re-aligning search intent).
* **Cost of Wrong Calls:**
  * *False Positive (Flagging a healthy page):* Wasted editorial hours spent auditing pages that do not need intervention, creating an opportunity cost.
  * *False Negative (Missing a declining page):* Unnoticed traffic decay compounding over months until recovering search position requires a complete, expensive rewrite.

### C. Live Dataset Evidence (30,000 Anonymized Pages)
Executed live Python data verification against `data/raw/content_refresh_anonymized.csv`:

```text
=== LIVE DATASET ANALYSIS (data/raw/content_refresh_anonymized.csv) ===
1. Total Pages Analyzed:      30,000
2. Overall Declining Pages:    16,262 (54.21% of total inventory)
3. Visible Pages (imp >= 100): 22,006 (73.35% of total inventory)
4. Declining Visible Pages:    13,152 (59.77% of visible demand)
```

* **Key Takeaway:** Over **13,000 visible pages** are currently experiencing downward traffic trends. This massive backlog proves that manual inspection cannot scale and justifies an ML-based decision support system.

### D. Claim Boundaries & Scope Control
* **What We CAN Claim:**
  * Observational correlations between content features and decline.
  * Probabilistic ranking of pages by decline risk.
  * Decision-support recommendations for human reviewers.
* **What We CANNOT Claim:**
  * Causal proof (we cannot claim a refresh *causes* recovery without controlled A/B testing).
  * Reverse-engineering search engine algorithms ("predicting Google").

---

## 💡 3. What I Learned

### Key Mastery Takeaways:

1. **Problem-First Machine Learning:**
   * A successful ML project does not begin with selecting algorithms or tuning hyperparameters. It begins by answering: *What human decision does this improve, who acts on it, and what is the cost of being wrong?*

2. **The Importance of Grain:**
   * Understanding the exact grain of the dataset (here: 1 row = 1 content page `content_id`) is essential before joining tables, aggregating signals, or building target labels.

3. **Decision Support vs. Pure Automation:**
   * Real-world applied ML in complex domains (like search content) is rarely about 100% automated decision-making. The model serves as a **decision-support filter** that orders options for human expert review.

4. **Quantifying Operational Backlog:**
   * Learned how to use descriptive data analysis to quantify problem magnitude (e.g. discovering that 59.77% of active demand pages are declining) to justify engineering investment.

5. **Epistemic Humility & Communication:**
   * Mastered careful language boundaries. Communicating clearly what a statistical model can claim (observational trends, ranking probability) versus what it cannot (causal proof, algorithm reverse-engineering) is critical for professional data science deliverables.
