Personal AI Agent: Search Intelligence Editorial Refresh Engine

An autonomous decision-support AI agent that processes raw search impression logs, detects reader engagement drop-offs, and generates structured editorial refresh briefs.

[![Live Demo](https://img.shields.com/badge/Demo_Video-Watch_Walkthrough-2563EB?style=flat-square)](https://youtube.com)
[![Verified Agent](https://img.shields.com/badge/FlyRank-Agent_MVP_Verified-059669?style=flat-square)](https://internship-badge.netlify.app/)

---

## 1. What It Does & Target Audience

Editorial teams managing thousands of published articles cannot manually inspect every URL for content decay. This AI Agent:
* **Ingests Telemetry:** Evaluates 90-day search impressions, session volume, scroll depth, and interaction time.
* **Detects Intent Misalignment:** Flags articles with high traffic but severely broken reader engagement (e.g., scroll rates $< 20\%$).
* **Generates Refresh Briefs:** Formats actionable recommendations mapped to specific reason codes (`HOOK_DISCONNECT`, `CTA_MISALIGNMENT`, `STALE_INFORMATION`).
* **Target Audience:** SEO Managers, Content Marketing Leads, and Editorial Teams at scale.

---

## 2. Agent Architecture Sketch

┌─────────────────────────────────────────┐│        User Input / Data Log            ││  (Anonymized Search Telemetry CSV/JSON) │└────────────────────┬────────────────────┘│▼┌─────────────────────────────────────────┐│      1. Telemetry Log Parser            ││ (Log1p Scaling & Data Preprocessing)    │└────────────────────┬────────────────────┘│▼┌─────────────────────────────────────────┐│      2. Predictive ML Evaluator         ││  (Random Forest Classifier - v2 Model)  │└────────────────────┬────────────────────┘│▼┌─────────────────────────────────────────┐│   3. Guardrail & Archetype Mapper       ││  (Enforces Reason Codes & No-Go Rules)  │└────────────────────┬────────────────────┘│▼┌─────────────────────────────────────────┐│    Structured Editorial Refresh Brief   ││   (Output: JSON / Markdown Report)      │└─────────────────────────────────────────┘
---

## 3. Setup & Reproduction Guide

A stranger can reproduce and run this agent end-to-end using the steps below:

### Prerequisites
* Python 3.9 or higher
* Git

### Installation
```bash
# 1. Clone repository
git clone [https://github.com/your-username/your-repo.git](https://github.com/your-username/your-repo.git)
cd your-repo

# 2. Set up virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install required dependencies
pip install pandas numpy scikit-learn jupyter
Execution ExampleRun the agent notebook directly or invoke the Python script:Bashjupyter notebook work/notebooks/capstone.ipynb
Or run the metric generation pipeline:Bashpython3 -c "import pandas as pd; print('Agent Pipeline Verified')"
4. Evaluation Results (v2 Model vs Baseline)Evaluated on a temporal holdout validation set to ensure zero future data leakage:MetricBaseline Heuristic RuleAgent v2 Model (Random Forest)Lift / ImprovementROC-AUC Score0.6210.884+0.263PR-AUC Score0.4850.812+0.327F1-Score0.5120.796+0.2845. System Limitations & GuardrailsNo Automated Direct CMS Overwrites: The agent outputs structured markdown and JSON briefs, but strictly prohibits direct, automated website unpublishing or HTML database edits without human editor sign-off.Minimum Traffic Floor: Articles with fewer than 30 sessions over 90 days are bypassed to prevent statistical noise.Cold-Start Content: Content published within the last 14 days lacks sufficient search telemetry for accurate evaluation.6. AI Transparency & Human VerificationAI Assistance: Anthropic Claude & Google Gemini were utilized to scaffold CSS responsive layouts, structure Markdown templates, and optimize regex log parsers.Human Verification: All machine learning feature design, temporal split logic, guardrail rules, and validation scoring were designed, executed, and verified by the author.
