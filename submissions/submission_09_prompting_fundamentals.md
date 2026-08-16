# 📑 Submission 9 — Phase: Foundations & AI Fluency (FL-02: Prompting Fundamentals v2)

**Task Reference:** `Foundations — Prompting Fundamentals on Real Tasks v2 (AI Fluency Week 2)`  
**Phase:** Foundations / AI Fluency | **Estimated Hours:** 6  
**Deliverable File:** [`submissions/submission_09_prompting_fundamentals.md`](submissions/submission_09_prompting_fundamentals.md)

---

## 🎯 1. Assignment Objectives

The primary goals of this prompt engineering assignment were:
1. **Target Task Selection:** Select one real recurring task from the FL-01 Workflow Audit (*Automated Data Contract Verification & Feature Leakage Audit*).
2. **5+ Technique Iterations:** Build a 6-run prompt progression starting from a naive one-line prompt (V0) through five iterations, each applying one named technique:
   * V1: **Role Assignment**
   * V2: **Context & Motivation**
   * V3: **Few-Shot Examples**
   * V4: **Output Structure**
   * V5: **Step Decomposition**
3. **Observed Output Differences:** Write evaluation notes for each version detailing what improved in the actual LLM output rather than just describing the prompt text.
4. **Honest Cross-Model Comparison:** Run the final prompt on both Claude (Claude 3.5/3.7) and ChatGPT (GPT-4o) and compare tone, accuracy, structure adherence, and failure points.
5. **Reusable Template Asset:** Distill the result into a clean, portable prompt template usable by anyone without personal context.

---

## 🪜 2. The 6-Version Prompt Iteration Log

---

### 🔴 Naive Version (V0) — One-Line Baseline

#### The Prompt:
> *"Audit this search data for leakage and write a data contract."*

#### Representative Output Excerpt:
> "Feature leakage occurs when data from the target variable enters the training set. To write a data contract, ensure that target columns are removed and column types match. A data contract specifies column names, data types, and nullability rules for your database tables..."

#### Evaluation Note:
* **Technique Applied:** None (Naive baseline).
* **Observed Output Difference:** The LLM produced generic textbook definitions of feature leakage and data contracts without referencing real files, specific columns, or executable Python assertions.

---

### 🟡 Version 1 (V1) — Technique: **Role Assignment**

#### The Prompt:
> *"Act as a Lead Data Quality Architect and Senior ML Systems Engineer. Audit this search performance dataset for feature leakage and write a production-grade data contract."*

#### Representative Output Excerpt:
> "As Data Quality Architect, I have structured this dataset audit to evaluate schema stability, leakage boundaries, and contract constraints. 1. Schema Validation... 2. Leakage Audit..."

#### Evaluation Note:
* **Technique Applied:** **Role Assignment**
* **Observed Output Difference:** The tone shifted from conversational textbook explanations to authoritative engineering prose. Output was structured under formal architectural headers, though still lacked specific dataset schemas.

---

### 🟢 Version 2 (V2) — Technique: **Context & Motivation**

#### The Prompt:
> *"Act as a Lead Data Quality Architect. Audit FlyRank's 30,000-row search performance dataset `data/raw/content_refresh_anonymized.csv` (grain: 1 row = 1 `content_id`). Motivation: `trend_direction` and `trend_pct` are derived directly from the 30-day future performance window. If these columns leak into model features, models achieve fake 100% accuracy in training but fail completely in production on client-holdout splits."*

#### Representative Output Excerpt:
> "CRITICAL LEAKAGE ALERT: Columns `trend_direction` and `trend_pct` are target-derived artifacts. 
> Prohibited Feature List: [`trend_direction`, `trend_pct`]. 
> Allowed Input Features: [`impressions_90d`, `clicks_90d`, `ctr`, `avg_position`, `content_age_days`, `days_since_last_update`].
> Grouping Rule: Split train/test sets on `client_id` to prevent cross-domain leakage."

#### Evaluation Note:
* **Technique Applied:** **Context & Motivation**
* **Observed Output Difference:** The output immediately identified the exact prohibited columns (`trend_direction`, `trend_pct`), explained why they create target leakage, and explicitly mandated `client_id` grouped splits.

---

### 🔵 Version 3 (V3) — Technique: **Few-Shot Examples**

#### The Prompt:
> *[V2 Prompt]*  
> *"Example of expected YAML contract output:*
> ```yaml
> dataset_name: content_refresh_anonymized
> grain: content_id
> prohibited_features:
>   - trend_direction
>   - trend_pct
> assertions:
>   - column: ctr
>     type: float
>     min: 0.0
>     max: 100.0
> ```"

#### Representative Output Excerpt:
```yaml
dataset_name: content_refresh_anonymized
grain: content_id
client_identifier: client_id
prohibited_features:
  - trend_direction
  - trend_pct
value_constraints:
  - column: avg_position
    type: float
    special_value_note: "0.0 indicates no search data, not rank zero"
  - column: impressions_90d
    type: integer
    min: 0
  - column: scroll_rate
    type: float
    note: "Can exceed 100 due to cross-system analytics tracking"
```

#### Evaluation Note:
* **Technique Applied:** **Few-Shot Examples**
* **Observed Output Difference:** The LLM adopted the exact YAML schema structure provided in the example and correctly incorporated FlyRank-specific data dictionary gotchas (e.g. `avg_position = 0` meaning no data).

---

### 🟣 Version 4 (V4) — Technique: **Output Structure Enforcement**

#### The Prompt:
> *[V3 Prompt]*  
> *"Output Format Constraint: Return strictly a 4-section Markdown document with no conversational introduction or conclusion:*
> *Section 1: Data Contract YAML Metadata*
> *Section 2: Target Leakage Blacklist Table*
> *Section 3: Column Constraint & Gotchas Matrix*
> *Section 4: Python Verification Assertion Script"*

#### Representative Output Excerpt:
```markdown
# Section 1: Data Contract YAML Metadata
[YAML block...]

# Section 2: Target Leakage Blacklist Table
| Prohibited Column | Derivation Source | Operational Risk |
|---|---|---|
| trend_direction | Computed from trend_pct | Direct Target Leakage |
| trend_pct | Windowed impression delta | Future Outcome Leakage |

# Section 3: Column Constraint Matrix
[Matrix table...]

# Section 4: Python Verification Assertion Script
[Python script block...]
```

#### Evaluation Note:
* **Technique Applied:** **Output Structure Enforcement**
* **Observed Output Difference:** Completely eliminated conversational intros ("Sure, here is your audit...") and produced a standardized, copy-pasteable technical document matching the 4 required sections.

---

### ⚪ Version 5 (V5) — Technique: **Step Decomposition (Chain-of-Thought)**

#### The Prompt:
> *[V4 Prompt]*  
> *"Before generating the final contract, execute step-by-step reasoning in a `<thinking>` block:*
> *Step 1: Parse dataset schema and identify candidate features vs target outcomes.*
> *Step 2: Trace target derivation math to flag hidden leakage columns.*
> *Step 3: Check data dictionary gotchas (percentage multipliers, position 0 flags, missingness patterns).*
> *Step 4: Construct assertions and validation Python code."*

#### Representative Output Excerpt:
```xml
<thinking>
Step 1: Dataset contains 44 columns across search volume, engagement, and trend metrics.
Step 2: trend_pct = (impressions_last_30d - impressions_prev_30d) / impressions_prev_30d. This is the exact target window! Flagging trend_pct and trend_direction as Prohibited.
Step 3: ctr, engagement_rate, scroll_rate are percentages * 100 (e.g. 0.76 = 0.76%). avg_position = 0 represents missing rank data.
Step 4: Writing Python assert statements for non-null content_id, unique grain, and leakage exclusions.
</thinking>

# Section 1: Data Contract YAML Metadata...
```

#### Evaluation Note:
* **Technique Applied:** **Step Decomposition (Chain-of-Thought)**
* **Observed Output Difference:** The explicit reasoning step caused the model to catch subtle edge cases (e.g., noting that percentage columns are scaled $\times 100$) before compiling the final contract assertions.

---

## ⚔️ 3. Cross-Model Comparison (Claude vs. ChatGPT)

The final V5 engineered prompt was executed on both **Claude (Claude 3.5 Sonnet / 3.7)** and **ChatGPT (GPT-4o)**.

| Evaluation Dimension | Claude (Claude 3.5 Sonnet / 3.7) | ChatGPT (GPT-4o) |
|---|---|---|
| **Tone & Style** | Direct, precise, systems-oriented; strictly adhered to output structure with zero conversational fluff. | Professional but slightly verbose; added brief introductory and concluding remarks despite format constraints. |
| **Leakage Detection Accuracy** | Flawless; correctly identified `trend_direction` and `trend_pct` and flagged subtle leakage risks in windowed metrics. | Identified main leakage columns, but initially suggested imputing missing trend values rather than strictly excluding them. |
| **Format Adherence** | 100% compliance with `<thinking>` block tag and the 4 markdown section boundaries. | Followed markdown section headers well, but placed the `<thinking>` section inside a standard code block rather than raw XML tags. |
| **Code Executability** | Produced clean, modular Python assertions using `pandas` and `assert` statements ready for CI integration. | Produced valid Python code, but used `df.dropna()` indiscriminately, which would drop valid rows with missing keyword data. |
| **Failure Point Summary** | Missed adding inline docstrings to the Python assertion functions unless explicitly requested. | Tendency to over-explain code blocks with conversational text beneath code snippets. |

---

## 🚀 4. Final Reusable Prompt Template

Below is the portable, reusable prompt template designed for data engineers to audit search telemetry datasets:

```text
SYSTEM ROLE:
You are a Senior Data Quality Architect specializing in data contracts and feature leakage prevention.

TASK OBJECTIVE:
Audit a search performance dataset, establish a strict data contract, and generate automated Python verification assertions.

DATASET INPUT CONTEXT:
- Dataset File: {DATASET_PATH}
- Dataset Grain: 1 row = 1 {GRAIN_ID}
- Client Grouping Column: {CLIENT_ID_COL}
- Target Outcome Description: {TARGET_DESCRIPTION}

EXECUTION STEPS (Decomposition):
Execute step-by-step reasoning inside a <thinking> block:
1. Identify all target-derived columns and mark them as PROHIBITED features.
2. Check scale multipliers (percentages, position zero flags) and missingness patterns.
3. Formulate value range constraints and grain uniqueness rules.
4. Construct executable Python assertion code.

OUTPUT FORMAT REQUIREMENTS:
Return strictly the following 4 sections:
# Section 1: Data Contract Metadata (YAML format)
# Section 2: Prohibited Feature Blacklist (Table: Column | Source | Risk)
# Section 3: Column Constraint Matrix (Table: Column | Type | Allowed Range | Gotchas)
# Section 4: Python Data Contract Assertion Script (Executable pandas code)
```

---

## 💡 5. What I Learned

1. **Chain-of-Thought Catches Edge Cases:** Adding `<thinking>` step decomposition prevented the model from rushing into code and caught subtle schema gotchas (`avg_position = 0`).
2. **Few-Shot Examples Mandate Structure:** Providing a small YAML exemplar was far more effective at enforcing schema syntax than descriptive instructions alone.
3. **Cross-Model Nuance:** Claude excels at strict format adherence and precise code assertions, while ChatGPT provides broader context but requires tighter constraints against conversational fluff and improper `fillna` logic.
