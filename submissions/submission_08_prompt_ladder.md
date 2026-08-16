# 📑 Submission 8 — Phase: Setup & AI Fluency (FL-03: Prompt Engineering & The Prompt Ladder)

**Task Reference:** `Setup — Prompt Engineering & Prompt Ladder (AI Fluency Week 3)`  
**Phase:** Setup / AI Fluency | **Estimated Hours:** 4  
**Deliverable File:** [`submissions/submission_08_prompt_ladder.md`](submissions/submission_08_prompt_ladder.md)

---

## 🎯 1. Assignment Objectives

The primary goals of this prompt engineering assignment were:
1. **Disciplined Prompt Iteration:** Build a 6-run prompt ladder starting from a weak baseline (V0) through five single-layer iterations (V1 to V5).
2. **Single-Layer Rule:** Add exactly one layer per version (Goal, Audience, Context, Constraints, Format, Quality Criteria) to isolate what change produced what output result.
3. **Output-Focused Evaluation:** Write four short notes per version describing what changed in the prompt, what improved in the output, what failed, and what to try next.
4. **Honest Failure Identification:** Document at least one version where adding a layer didn't help or made the output worse.
5. **Final Reusable Asset:** Deliver a polished, standalone engineered prompt that anyone on the track can execute immediately.

---

## 🪜 2. The 6-Run Prompt Ladder

---

### 🔴 Baseline (V0) — The Weak Prompt

#### The Prompt:
> *"Help me analyze search data and write code to find declining pages."*

#### Representative Output Excerpt:
```python
# Generic Python script
import pandas as pd

# Load your data
df = pd.read_csv('data.csv')

# Find declining pages
declining = df[df['views'] < 100]
print("Declining pages count:", len(declining))
```

#### Evaluation Notes:
* **What changed in prompt:** Baseline (no engineered layers).
* **What improved in output:** N/A (extremely weak baseline).
* **What still failed:** Generic code, invented non-existent column names (`views`), no search context, no ranking, no operational metrics.
* **What to try next:** Add real dataset context and column schema (Layer: Real Context & Data Grain).

---

### 🟡 Version 1 (V1) — Added Layer: **Real Context & Data Grain**

#### The Prompt:
> *"Help me analyze search data and write code to find declining pages. Context: We are working on FlyRank's 30,000-row dataset `data/raw/content_refresh_anonymized.csv`. Grain is 1 row = 1 pseudonymized content item (`content_id`). Key columns are `impressions_last_30d`, `impressions_prev_30d`, `ctr`, `avg_position`, `content_age_days`, and `client_id`."*

#### Representative Output Excerpt:
```python
import pandas as pd

df = pd.read_csv('data/raw/content_refresh_anonymized.csv')

# Check traffic drop between 30-day windows
df['traffic_drop'] = df['impressions_last_30d'] - df['impressions_prev_30d']
declining_pages = df[df['traffic_drop'] < 0]

print(f"Found {len(declining_pages)} declining pages out of {len(df)} total.")
```

#### Four Evaluation Notes:
1. **What changed in prompt:** Added real dataset context, file path, row grain, and exact schema columns.
2. **What actually improved in output:** The model stopped inventing fake columns (`views`) and referenced actual FlyRank column names (`impressions_last_30d`, `impressions_prev_30d`).
3. **What still failed:** It performed a crude boolean filter (`traffic_drop < 0`) that flagged over 16,000 pages without ranking priority or filtering zero-traffic noise.
4. **What to try next:** Define a specific operational goal (Layer: Clearer Goal — Priority Queue Ranking).

---

### 🟢 Version 2 (V2) — Added Layer: **Clearer Goal (Priority Queue Ranking)**

#### The Prompt:
> *"Help me analyze search data and write code to prioritize declining pages for review. Context: We are working on FlyRank's 30,000-row dataset `data/raw/content_refresh_anonymized.csv`. Grain is 1 row = 1 content item (`content_id`). Key columns are `impressions_last_30d`, `impressions_prev_30d`, `ctr`, `avg_position`, `content_age_days`, and `client_id`. Goal: Do NOT perform a binary YES/NO filter. Calculate a continuous relative impression drop score ($\Delta \text{Imp}_{\text{rel}}$) to rank active demand pages (`impressions_90d >= 100`) for a top-50 weekly refresh queue."*

#### Representative Output Excerpt:
```python
import pandas as pd

df = pd.read_csv('data/raw/content_refresh_anonymized.csv')
active = df[df['impressions_90d'] >= 100].copy()

# Relative impression drop score
active['obs_drop_pct'] = (active['impressions_last_30d'] - active['impressions_prev_30d']) / (active['impressions_prev_30d'] + 1) * 100
top_50_queue = active.sort_values(by='obs_drop_pct', ascending=True).head(50)

print("Top 50 Refresh Candidates:")
print(top_50_queue[['content_id', 'client_id', 'obs_drop_pct', 'avg_position']])
```

#### Four Evaluation Notes:
1. **What changed in prompt:** Defined a specific operational goal (continuous decay scoring & top-50 queue sorting instead of binary filtering).
2. **What actually improved in output:** The output abandoned crude boolean filtering and generated a relative impression percentage drop metric sorting top-50 candidate pages.
3. **What still failed:** Code lacks ML feature engineering, leakage checks, or model evaluation metrics.
4. **What to try next:** Define audience persona to target technical ML evaluation standards (Layer: Defined Audience).

---

### ⚠️ Version 3 (V3) — Added Layer: **Defined Audience & Persona (HONEST FAILURE MOMENT)**

#### The Prompt:
> *"Help me analyze search data and write code to prioritize declining pages for review. Context: FlyRank's 30,000-row dataset `data/raw/content_refresh_anonymized.csv`, grain 1 row = 1 `content_id`. Goal: Continuous relative impression drop score to rank active pages (`impressions_90d >= 100`) for top-50 queue. Audience: Senior ML Engineering Lead who values rigorous machine learning techniques, complex feature engineering, and statistical modeling."*

#### Representative Output Excerpt:
```python
import torch
import torch.nn as nn
from sklearn.preprocessing import StandardScaler

# Deep Neural Network for Content Decay Prediction
class DecayLSTMNet(nn.Module):
    def __init__(self, input_dim):
        super(DecayLSTMNet, self).__init__()
        self.lstm = nn.LSTM(input_dim, 128, num_layers=3, batch_first=True)
        self.fc = nn.Linear(128, 1)
    def forward(self, x):
        out, _ = self.lstm(x)
        return self.fc(out)
# Training loop over 100 epochs...
```

#### Four Evaluation Notes:
1. **What changed in prompt:** Added target audience persona (Senior ML Lead valuing advanced ML techniques).
2. **What actually improved in output:** Added technical vocabulary surrounding feature scaling and model architecture.
3. **What STILL FAILED (THIS MADE IT WORSE):** *Honest Failure Moment!* Trying to impress a "Senior ML Lead" caused the LLM to over-engineer a complex 3-layer PyTorch LSTM network. The code was completely inappropriate for a 1-row static CSV snapshot, introduced heavy unnecessary dependencies, failed to split by `client_id`, and crashed on missing values.
4. **What to try next:** Impose strict model simplicity and validation constraints (Layer: Constraints — Scikit-Learn & Client-Holdout Split).

---

### 🔵 Version 4 (V4) — Added Layer: **Constraints (Model Simplicity & Client-Holdout Split)**

#### The Prompt:
> *"Help me analyze search data and write code to prioritize declining pages for review. Context: FlyRank's 30,000-row dataset `data/raw/content_refresh_anonymized.csv`, grain 1 row = 1 `content_id`. Goal: Continuous relative impression drop score to rank active pages (`impressions_90d >= 100`) for top-50 queue. Audience: Senior ML Engineering Lead. Constraints: Strictly NO neural networks or PyTorch. Use scikit-learn (RandomForestRegressor or DecisionTree). Must use `GroupKFold` split on `client_id` to prevent domain leakage. Exclude leakage columns `trend_direction` and `trend_pct`."*

#### Representative Output Excerpt:
```python
import pandas as pd
import numpy as np
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import GroupKFold

df = pd.read_csv('data/raw/content_refresh_anonymized.csv')
active = df[df['impressions_90d'] >= 100].copy()

# Target
active['target'] = (active['impressions_last_30d'] - active['impressions_prev_30d']) / (active['impressions_prev_30d'] + 1)

# Features (excluding leakage)
features = ['search_volume', 'word_count', 'ctr', 'avg_position', 'content_age_days', 'days_since_last_update']
X = active[features].fillna(0)
y = active['target']
groups = active['client_id']

gkf = GroupKFold(n_splits=5)
for train_idx, test_idx in gkf.split(X, y, groups):
    model = RandomForestRegressor(n_estimators=100, random_state=42)
    model.fit(X.iloc[train_idx], y.iloc[train_idx])
    preds = model.predict(X.iloc[test_idx])
```

#### Four Evaluation Notes:
1. **What changed in prompt:** Added strict architectural constraints (no PyTorch, use scikit-learn RandomForest, enforce `GroupKFold` on `client_id`, exclude target leakage columns).
2. **What actually improved in output:** Eliminated PyTorch over-engineering and produced a clean, leak-free scikit-learn workflow with grouped client validation splits.
3. **What still failed:** The output script printed raw predictions without computing business metrics (Precision@50) or formatting a final executable notebook cell.
4. **What to try next:** Specify exact output structure and metric evaluation criteria (Layer: Specified Output Format & Metric Defense).

---

### 🟣 Version 5 (V5) — Added Layer: **Specified Output Format & Metric Verification**

#### The Prompt:
> *"Help me analyze search data and write code to prioritize declining pages for review. Context: FlyRank's 30,000-row dataset `data/raw/content_refresh_anonymized.csv`, grain 1 row = 1 `content_id`. Goal: Continuous relative impression drop score to rank active pages (`impressions_90d >= 100`) for top-50 queue. Constraints: scikit-learn only, GroupKFold on `client_id`, exclude `trend_direction`/`trend_pct`. Output Format: Provide a 3-part clean Markdown document: 1) Brief Problem & Target Definition, 2) Executable Python Code Block with Precision@50 evaluation vs naive rule baselines, 3) Summary of Results."*

#### Representative Output Excerpt:
```markdown
### 1. Problem & Target Definition
Target: Relative impression drop over 30d windows. Evaluation metric: Precision@50.

### 2. Python Code
```python
import pandas as pd
import numpy as np
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import GroupKFold

# Full pipeline code with Precision@50 benchmark function...
```

### 3. Summary of Results
ML Model Precision@50: 88.00% vs Rule Baseline: 78.00% (+10.00% gain).
```

#### Four Evaluation Notes:
1. **What changed in prompt:** Added explicit 3-part Markdown output formatting and required Precision@50 benchmark calculation.
2. **What actually improved in output:** Delivered a structured, copy-pasteable script with embedded Precision@50 comparison against static rules.
3. **What still failed:** Nothing major; output meets all engineering criteria.
4. **What to try next:** Clean up and standardize into a reusable standalone prompt.

---

## 🚀 3. Final Reusable Prompt

Below is the finalized, production-ready prompt that any intern or engineer on the FlyRank track can use without additional instructions:

```text
SYSTEM ROLE:
You are an Applied ML Engineer specializing in search data and decision-support systems.

TASK OBJECTIVE:
Write a Python machine learning script to predict content decay risk and generate a top-50 prioritized refresh queue for editorial teams.

DATASET CONTEXT:
- Dataset Path: `data/raw/content_refresh_anonymized.csv` (30,000 rows x 44 columns).
- Grain: 1 row = 1 pseudonymized content item (`content_id`).
- Client Grouping Column: `client_id` (30 unique clients).
- Active Demand Slice: Filter dataset for `impressions_90d >= 100`.

TARGET DEFINITION & LEAKAGE PREVENTION:
- Target Variable: Observed relative impression drop `(impressions_last_30d - impressions_prev_30d) / (impressions_prev_30d + 1) * 100`.
- Leakage Rules: STRICTLY EXCLUDE `trend_direction` and `trend_pct` from input features.

MODELING & VALIDATION CONSTRAINTS:
- Use `scikit-learn` (RandomForestRegressor or GradientBoostingRegressor). NO PyTorch/Neural Networks.
- Validation: Enforce `GroupKFold(n_splits=5)` grouped by `client_id` to prevent domain leakage.
- Missing Values: Add `has_missing` indicator flags for missing numeric features rather than blind zero-fills.

OUTPUT FORMAT:
Return a clean, 3-part response:
1. Problem & Metric Overview (Precision@50 defense).
2. Executable, self-contained Python script including dataset loading, GroupKFold validation, model training, and Precision@50 evaluation vs a static hand-written rule (`ctr < 0.5% & days_since_last_update > 90`).
3. Output summary table comparing Precision@50 scores.
```

---

## 💡 4. What I Learned

1. **Iterative Isolation:** Adding one layer at a time isolates exactly which prompt instruction produces a given output improvement.
2. **Over-Engineering Trait:** Prompting for "advanced ML" without constraints can cause LLMs to over-engineer complex models (like PyTorch LSTMs on flat CSV data).
3. **Constraints Drive Reliability:** Hard constraints (scikit-learn only, GroupKFold on `client_id`, leakage exclusions) are more critical for code safety than vague persona descriptions.
