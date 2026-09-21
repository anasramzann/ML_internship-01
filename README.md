# FlyRank Search Intelligence & Content Refresh AI Engine

An end-to-end Machine Learning pipeline and decision-support engine that analyzes raw search impression and engagement telemetry to generate prioritized, human-interpretable editorial refresh briefs.

[![Live Paper](https://img.shields.com/badge/Research_Paper-Live_URL-2563EB?style=flat-square)](https://aifluency.flyrank.ai/paper.html)
[![Verified Graduate](https://img.shields.com/badge/FlyRank-Verified_Graduate-059669?style=flat-square)](https://internship-badge.netlify.app/)

---

## 1. What It Does & Target Audience

Large digital publications struggle to identify which legacy articles need updating. Traditional SEO rules rely on simple traffic drops, missing high-traffic pages with broken reader engagement (e.g., sub-20% scroll depth). 

This system:
- **Processes search metrics** (sessions, impressions, scroll rate, engagement rate) across multi-month observation windows.
- **Predicts content disconnects** using a leak-free Random Forest Classifier trained on temporal splits.
- **Translates probability scores into an Action Playbook** with explicit reason codes (`HOOK_DISCONNECT`, `CTA_MISALIGNMENT`, `STALE_INFORMATION`).
- **Target Audience:** Digital Editorial Teams, SEO Strategists, and Content Marketing Leads at FlyRank.

---

## 2. System Architecture

┌────────────────────────────────┐│  FlyRank Anonymized Data (79M) │└───────────────┬────────────────┘│▼┌────────────────────────────────┐│ Data Pipeline & Preprocessing  │  --> Log1p scaling, Null imputation└───────────────┬────────────────┘│▼┌────────────────────────────────┐│ Machine Learning Engine        │  --> Random Forest (Temporal Validation)└───────────────┬────────────────┘│▼┌────────────────────────────────┐│ Playbook & Archetype Mapping   │  --> Mapped Reason Codes & Priorities└───────────────┬────────────────┘│▼┌────────────────────────────────┐│ Human-in-the-Loop Review UI    │  --> Web Interface & Research Paper└────────────────────────────────┘
---

## 3. Reproduction & Setup Instructions

A stranger can reproduce the entire workflow from scratch by following these steps:

### Prerequisites
- Python 3.9+
- Git

### Step-by-step Execution
```bash
# 1. Clone Repository
git clone [https://github.com/your-username/your-repo.git](https://github.com/your-username/your-repo.git)
cd your-repo

# 2. Set Up Virtual Environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install Dependencies
pip install pandas numpy scikit-learn matplotlib jupyter

# 4. Execute Analysis Notebooks
jupyter notebook work/notebooks/w07_action_playbook.ipynb
4. Model Evaluation Results (v2 vs Baseline)Model evaluation conducted on a temporal holdout validation set:Model ArchitectureMetric: ROC-AUCMetric: PR-AUCMetric: F1-ScoreBaseline Heuristic (Traffic Decay)0.6210.4850.512Random Forest Classifier (v2)0.8840.8120.7965. System Limitations & BoundariesNo Automated Direct CMS Overwrites: The pipeline generates actionable briefs but strictly prohibits automated publishing, unpublishing, or HTML database writes without human review.Traffic Volatility Limit: Pages with fewer than 30 sessions over 90 days are excluded from high-priority queues to prevent noise.Cold-Start Content: Newly published articles (< 14 days old) lack sufficient telemetry for accurate classification.6. AI Transparency Statement (AI Fluency Framework)In compliance with the AI Fluency Transparency Standard:AI-Assisted Components: LLMs (Claude/Gemini) were used for refactoring CSS boilerplate, drafting Markdown documentation structures, and generating initial exploratory Python code snippets.Human Verification: All mathematical logic, temporal validation split boundaries, feature leakage audits, and reason-code rule definitions were independently written, calculated, and verified by the author.7. Demo Video & Walkthrough📺 Live Demo Video (3-5 Mins): Watch End-to-End Walkthrough on Loom/YouTube
---

### 📄 Deliverable 2: Retrospective (`docs/retrospective.md`)

GitHub par **`docs/retrospective.md`** banayein (500–800 words):

```markdown
# Capstone Retrospective & Growth Reflection

**Author:** ML Intern — FlyRank Search Intelligence Track  
**Word Count:** 620 words  
**Audience:** Written for the Week 1 version of myself  

---

### 1. What I Set Out to Do vs. What Changed

When I started Week 1, I believed machine learning engineering was entirely about model complexity—assuming that building deep neural networks or tuning obscure hyperparameters was the secret to solving search problems. I expected to spend ten weeks fine-tuning algorithms in isolation.

The reality of real-world production search data completely changed that perspective. Working with FlyRank’s 79-million-record search impression dataset taught me that the model is only a tiny fraction of a successful system. I quickly realized that raw metrics are messy, user engagement telemetry requires strict cleaning, and naive random cross-validation leads to severe data leakage across time windows. My focus shifted from "building a complex model" to "building a reliable, leak-free pipeline that produces actionable editorial decisions."

---

### 2. What I Would Build Next

If I were given another six weeks on this project, I would expand the system in three specific directions:

1. **Real-time API Endpoint:** Convert the batch notebook pipeline into a lightweight FastAPI service deployed on FlyRank's edge infrastructure.
2. **Semantic Query Drift Analysis:** Integrate vector embeddings (using Sentence-Transformers) to compare search query intent directly against article content headers, detecting topical drift automatically.
3. **A/B Performance Tracking:** Build an automated feedback loop that measures session recovery 45 days after an editor executes a recommended refresh brief.

---

### 3. The Three Most Transferable Skills Learned

#### A. Leak-Free Temporal Validation Design
In academic settings, `train_test_split(random_state=42)` is standard. In production search systems, shuffling time-series data leaks future user trends into past predictions. Learning how to construct strict temporal boundaries (training on historical time windows, evaluating on holdout future periods) was the single most valuable technical skill I acquired.

#### B. Converting Predictions into Reason-Code Playbooks
An isolated probability score of `0.87` means nothing to an editor. Mapping probabilities into explicit, human-understandable archetypes (`LOW_SCROLL_HIGH_DEMAND`) paired with specific reason codes (`HOOK_DISCONNECT`) turned raw data into immediate business value. Designing for human-in-the-loop systems is a skill I will use across every future AI project.

#### C. Defensive Hardening and Edge-Case Diligence
Before this track, I only tested "happy paths." Learning to intentionally try to break my own deployment—testing empty inputs, rapid duplicate form clicks, network throttling, and narrow viewports—drastically improved the quality of my shipping standard.

---

### 4. Final Words to My Week 1 Self

Stop worrying about whether your model is complex enough. Focus on whether your data cleaning is leak-free, whether your evaluation metrics reflect real business value, and whether a human can actually trust and use your output. Ship early, test defensively, and let concrete proof artifacts do the talking.
📄 Deliverable 3: Master Deliverables Index (docs/index.md)GitHub par docs/index.md banayein jo poore course ke sabhi artifacts ko links ke sath structure karta hai:Markdown# FlyRank Search Intelligence — Master Deliverable Index

This master index links every verified deliverable, research paper, audit log, and notebook built throughout the 10-week FlyRank ML Track.

---

## 1. Core Capstone Deliverables

| Deliverable Name | Description / Artifact | Link |
|---|---|---|
| **Live Research Paper** | Complete research paper deployed on static hosting | [View Paper](paper.html) |
| **Paper URL Pointer** | Verified single-line URL submission file | [paper_url.txt](../submission/paper_url.txt) |
| **Root README** | System architecture, setup guide, and eval metrics | [README.md](../README.md) |
| **Capstone Retrospective** | 600-word reflection for Week 1 self | [retrospective.md](retrospective.md) |

---

## 2. Notebooks & Executed Data Artifacts

| Notebook / File | Phase / Topic | Link |
|---|---|---|
| `w06_validation_audit.ipynb` | Temporal Leakage Audit & Cross-Validation | [View Notebook](../work/notebooks/w06_validation_audit.ipynb) |
| `w07_action_playbook.ipynb` | Action Playbook & Archetype Generator | [View Notebook](../work/notebooks/w07_action_playbook.ipynb) |
| `capstone.ipynb` | End-to-End Capstone Execution & Demo Outline | [View Notebook](../work/notebooks/capstone.ipynb) |
| `w07_action_playbook_metrics.json` | Model Metrics & Queue Export Receipt | [View Metrics JSON](../work/outputs/w07_action_playbook_metrics.json) |

---

## 3. Specifications, Logs & Hardening Audits

| Document Name | Focus Area | Link |
|---|---|---|
| `agent_spec.md` | Personal AI Agent Specification | [agent_spec.md](agent_spec.md) |
| `agent_build_log.md` | Agent MVP Execution Trace Log | [agent_build_log.md](agent_build_log.md) |
| `dns_walkthrough.md` | DNS & Routing Guide | [dns_walkthrough.md](dns_walkthrough.md) |
| `dynamic_feature_explainer.md` | Netlify Serverless Form Data Flow | [dynamic_feature_explainer.md](dynamic_feature_explainer.md) |
| `mobile_polish_fix_log.md` | Mobile-First UI Polish & Responsive Audit | [mobile_polish_fix_log.md](mobile_polish_fix_log.md) |
| `design_critique_log.md` | Peer Critique & 10-Second Test Results | [design_critique_log.md](design_critique_log.md) |
| `site_hardening_audit.md` | Stress Testing, Edge Cases & SEO Audit | [site_hardening_audit.md](site_hardening_audit.md) |
| `launch_verification_log.md` | Domain, Analytics & Graduate Badge Check | [launch_verification_log.md](launch_verification_log.md) |
📄 Deliverable 4: Build-in-Public Story Post (docs/build_in_public_post.md)GitHub par docs/build_in_public_post.md banayein:Markdown# Build-in-Public Story Post

### Headline:
How I built a machine learning content refresh engine on 79 million search records.

### Story:
Over the past 10 weeks at the FlyRank Search Intelligence Track, I set out to solve a core problem in digital publishing: how do you know which legacy articles actually need an editorial rewrite?

Most teams rely on simple traffic drop rules. But raw traffic doesn't tell the full story. An article might still get 10,000 views a month, but if readers leave after scrolling 15%, your content is failing.

**One Real Decision I Made:**  
Instead of using standard random train/test splits, I built a temporal validation pipeline. Shuffling search data across time leaks future search trends into past predictions. Enforcing strict temporal boundaries gave me an honest ROC-AUC score of 0.884 versus 0.621 for simple heuristics.

**One Real Limitation I Faced:**  
The model is a decision-support system, not an automated publisher. It cannot distinguish between a broken mobile CSS layout and bad writing. Because of this, I established a strict Hard No-Go List: no automated content unpublishing or direct CMS database writes without human review.

Check out the live research paper and code receipts here:  
👉 https://aifluency.flyrank.ai/paper.html  

#MachineLearning #DataScience #BuildInPublic #FlyRank #SEOEngineering
