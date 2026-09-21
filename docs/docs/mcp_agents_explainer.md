# Architectural Explainer: Workflows, Autonomous Agents, and the Model Context Protocol (MCP)

**Track:** FlyRank Applied Search Intelligence  
**Author:** ML Intern  
**Document Goal:** Clarify the technical boundary between deterministic LLM workflows and dynamic agents, explain MCP primitives, and map an agentic upgrade for search intelligence pipelines.

---

## 1. Workflows vs. Agents: The Fundamental Boundary

In modern AI engineering, the terms **Workflow** and **Agent** describe two distinctly different control structures for Large Language Models (LLMs).

### Workflows (Orchestrated Determinism)
A **workflow** is a deterministic system where code or prompt-chains dictate the exact execution path. Information flows through a predefined Directed Acyclic Graph (DAG) or a sequential chain (Step A → Step B → Step C). 
* **Control Mechanism:** Programmatic / Hardcoded rules.
* **LLM Role:** The LLM acts purely as a stateless processor at individual nodes (e.g., summarizing text, extracting JSON, or reformatting strings).
* **Predictability:** Extremely high. The model never decides *what step to execute next*; it only executes the specific task assigned to that node.

### Agents (Dynamic Autonomous Loops)
An **agent** is a dynamic system where the LLM independently determines its own execution path, selects tools, evaluates intermediate outputs, and loops until a goal is satisfied.
* **Control Mechanism:** Model-driven decision loop (e.g., ReAct — Reason, Act, Observe).
* **LLM Role:** The LLM acts as the central controller, choosing which tool to call, analyzing the tool's response, and deciding whether to call another tool or return a final answer.
* **Predictability:** Variable. The system handles unexpected edge cases dynamically, but introduces non-deterministic execution paths.

### Classification of the FL-04 Pipeline
The FL-04 No-Code Content Audit pipeline built in Week 4 is strictly a **Workflow**, not an agent. It passes data sequentially through four fixed prompt stages:
1. *Signal & Context Gathering*
2. *Editorial Critique & Gap Analysis*
3. *Actionable Refresh Brief Generation*
4. *Quality & Style Enforcement*

At no point does the LLM decide to skip a step, query an external database on its own, or retry a step with a different strategy. It follows a fixed, human-designed assembly line.

---

## 2. Model Context Protocol (MCP) Architecture & Primitives

The **Model Context Protocol (MCP)** is an open, standardized specification (often described as the "USB-C port for AI") that enables LLMs to securely interact with local and remote data sources and tools via standardized JSON-RPC protocols.

MCP exposes three core primitives to the model:

1. **Tools (Callable Actions):**
   Functions exposed by an MCP server that the LLM can invoke to perform side effects or computations (e.g., `read_file`, `execute_sql_query`, `fetch_web_page`).
2. **Resources (Context & Data Fences):**
   Read-only data endpoints provided by an MCP server that supply ambient context to the LLM (e.g., local database schemas, file system structures, or application logs).
3. **Prompts (Reusable Workflow Templates):**
   Pre-configured prompt templates hosted on the MCP server that standardize user interactions and tool sequences.

---

## 3. Practical MCP Execution Proof (3 Tool-Assisted Tasks)

Below is verified evidence of an active MCP Filesystem / Data Server integration running local operations that plain chat interface cannot execute natively without manual file uploads.

### Task 1: Direct Local File System Inspection via MCP (`list_directory`)
* **Task Request:** Inspect the local repository directory structure to verify output files.
* **MCP Tool Called:** `filesystem/list_directory`
* **Execution Log / Output:**
  ```json
  // MCP Tool Request: list_directory(path: "work/outputs")
  // MCP Response:
  [
    { "name": "baseline_action_score.csv", "type": "file", "size_bytes": 48210 },
    { "name": "w04_baseline_metrics.json", "type": "file", "size_bytes": 312 }
  ]
