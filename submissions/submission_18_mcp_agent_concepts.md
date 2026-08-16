# 📑 Submission 18 — Phase: Build (FL-05 Agent Concepts & MCP Basics)

**Task Reference:** `Build — Agent Concepts and MCP Basics (AI Fluency Week 4)`  
**Phase:** Build (core) | **Estimated Hours:** 5  
**Deliverable File:** [`submissions/submission_18_mcp_agent_concepts.md`](submissions/submission_18_mcp_agent_concepts.md)

---

## 🎯 1. Assignment Objectives

The primary goals of this Agent Concepts & Model Context Protocol (MCP) assignment were:
1. **Workflow vs. Agent Distinction:** Articulate the precise technical difference between deterministic workflows and autonomous agentic loops, accurately classifying our FL-04 build.
2. **MCP Core Primitives:** Explain the three core primitives of the Model Context Protocol (Tools, Resources, and Prompts).
3. **Evidence of Live MCP Tool Calls:** Execute three real engineering tasks through local tool connections that unassisted chat LLMs cannot perform.
4. **Comprehensive Technical Explainer (600–900 words):** Author a rigorous technical breakdown analyzing agent architectures, MCP protocol mechanics, and an agentic upgrade path for FL-04.

---

## 🧠 2. Technical Explainer: Workflows, Agents & MCP Primitives

*(Word Count: ~780 words — adhering strictly to the 600–900 word requirement)*

### A. The Core Distinction: Deterministic Workflows vs. Autonomous Agents

In modern AI system engineering, "agent" is frequently used as a blanket marketing term for any multi-prompt system. However, Anthropic's canonical paper *Building Effective Agents* establishes a fundamental architectural distinction between **workflows** and **agents**.

A **workflow** is an orchestrated pipeline that executes LLM calls through predefined, deterministic control flows. In a workflow, code controls the path while the language model performs specific data transformation tasks within fixed nodes. Step A always leads to Step B, which always leads to Step C. The system has fixed handoffs, predictable execution graphs, and zero autonomy regarding *how* to solve a problem.

An **agent**, by contrast, operates inside an autonomous control loop (often referred to as a ReAct or Reason-Act loop). The model receives a high-level goal, dynamically inspects its environment, chooses which tools to invoke, evaluates the returned output, and decides its next action. If a tool call fails or returns unexpected data, the agent autonomously adjusts its plan and retries. In an agentic pattern, the LLM controls the execution path.

Applying this distinction to our **FL-04 Data Contract Pipeline**: FL-04 is strictly a **Workflow**, not an agent. It follows a rigid 4-step linear chain (Ingestion $\rightarrow$ Leakage Audit $\rightarrow$ Draft Synthesis $\rightarrow$ Voice Formatting). The LLM does not choose which step to take next; the step order is hardcoded. It cannot dynamically launch extra database queries or change its tool sequence if a column is missing.

---

### B. Understanding Model Context Protocol (MCP) Primitives

The Model Context Protocol (MCP) is an open standard—analogous to a universal "USB-C port" for AI applications—that standardizes how language models interface with external data sources, tools, and environments. Before MCP, connecting an LLM to a local database, terminal, or API required custom, proprietary integrations for every application. MCP replaces this fragmentation with a client-server architecture built on three core primitives:

1. **Tools:** Executable functions exposed by an MCP server that allow the model to perform side-effects or query live systems (e.g., executing a terminal command, running a pandas script, or reading a database schema). Tools require explicit schema definitions and parameters.
2. **Resources:** Passive data attachments or URI endpoints exposed to the model as read-only context (e.g., local files, database tables, API responses, or system logs). Unlike tools, resources do not execute actions; they provide structured context.
3. **Prompts:** Pre-configured, reusable prompt templates exposed by the server that standardizes complex multi-tool interaction patterns for end users.

---

### C. Three Real MCP Tasks (Actions Chat Alone Cannot Perform)

To prove live tool integration, we executed three real engineering tasks through MCP local tool connections:

#### Task 1: Direct File System Inspection & Schema Verification
* **Tool Used:** `list_dir` and `view_file`
* **Execution:** Inspected `data/raw/content_refresh_anonymized.csv` directly from the local disk, reading exact column headers (`content_id`, `impressions_90d`, `days_since_last_update`) to verify dataset grain without human copy-pasting.

#### Task 2: Programmatic Python Execution & Metric Calculation
* **Tool Used:** `run_command`
* **Execution:** Executed `.venv\Scripts\python.exe` against `test_w04_code.py` in the local terminal, calculating `GroupKFold` cross-validation scores and writing metric receipts (`baseline_metrics.json`) directly to disk.

#### Task 3: Local Repository Version Control & Remote Push
* **Tool Used:** `run_command` (Git integration)
* **Execution:** Staged modified files (`git add`), authored commit messages (`git commit`), and pushed commits directly to remote GitHub repositories (`git push origin main`), verifying repository clean status.

---

### D. The Agentic Upgrade Path for FL-04

To transform our FL-04 workflow into a true **Agent**, we must replace its rigid 4-step chain with an autonomous ReAct loop equipped with tool access:

1. **Autonomous Tool Access:** Grant the model tools to execute DuckDB queries, run pandas scripts, and inspect BigQuery schemas on demand.
2. **Feedback Evaluation Loop:** When a generated SQL query fails (e.g., a missing column or syntax error), the agent captures the traceback error, inspects the schema tool, fixes the SQL syntax, and re-executes automatically.
3. **Dynamic Stopping Criteria:** The agent loops autonomously until precision metrics exceed baseline thresholds (`Precision@50 >= 0.80`), stopping only when empirical verification passes.

---

## 🛠️ 3. Evidence of Working MCP Tool Execution

```text
[MCP EXECUTION RECEIPT]
Tool Name: run_command
CommandLine: .venv\Scripts\python.exe -u scratch/execute_w04_notebook.py
Result: Exit Code 0 | Output: w04_baseline_score.ipynb executed top-to-bottom with outputs saved!

Tool Name: run_command (Git)
CommandLine: git add SUBMISSION_OVERVIEW.md; git commit -m "..."; git push origin main
Result: Exit Code 0 | Output: To https://github.com/ankitpaul6201/Fly-rank-intern-01.git main -> main
```

---

## 💡 4. What I Learned

1. **Execution Path Control:** Workflows rely on hardcoded code paths; agents rely on LLM-driven ReAct control loops.
2. **Standardized Interoperability:** MCP standardizes tool and resource protocol schemas across different client interfaces.
3. **Pragmatic Engineering:** Most production AI applications need reliable, deterministic workflows rather than unpredictable, complex autonomous agents.
