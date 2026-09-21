Markdown# Agent Design Specification: FlyRank Search Intelligence & Refresh Agent

**Project:** Personal AI Agent Capstone  
**Target Build Effort:** ~10 Hours  
**Track:** Applied Search Intelligence & ML Engineering  

---

## 1. Job to Be Done & User Persona

* **Job to Be Done:** Automatically audit engagement metrics (`sessions_90d`, `scroll_rate`, `engagement_rate`), prioritize underperforming search assets using trained model outputs (`w05_model_metrics.json`), diagnose search intent misalignment, and generate structured editorial refresh briefs for content creators.
* **Primary User:** ML Intern / Content Operations Lead at FlyRank.
* **Usage Frequency:** Weekly batch audit (every Monday) and on-demand ad-hoc page inspection.

---

## 2. Platform Selection & Architectural Justification

### Selected Platform: Claude Project + MCP (Model Context Protocol) / Local Python Runner
* **Why Selected:** Zero hosting costs, direct access to local repository datasets via MCP filesystem/data tools, and native integration with our established Identity Kit and prompt guardrails.
* **Comparison vs. Alternatives:**
  * *vs. Custom GPT (OpenAI):* Rejected due to requiring a paid ChatGPT Plus subscription and lack of native local filesystem MCP tooling.
  * *vs. n8n Autonomous Workflow:* Rejected due to setup complexity for a single-user weekly batch task where local execution via MCP provides tighter data contract safety.

---

## 3. Data Sources, Tools & Access Plan

| Asset / Tool Name | Type | Access Plan & Permissions | Purpose |
|---|---|---|---|
| `content_refresh_anonymized.csv` | Dataset | Local MCP Filesystem (Read-Only) | Raw search exposure and engagement metrics. |
| `w05_model_metrics.json` | Model Receipts | Local MCP Filesystem (Read-Only) | Model performance baseline and target thresholds. |
| `baseline_action_score.csv` | Priority Queue | Local MCP Filesystem (Read-Only) | Ranked action score output from Week 04/05. |
| `write_refresh_brief` | Output Tool | Local MCP Filesystem (Write) | Saves final Markdown brief into `work/outputs/briefs/`. |

---

## 4. Draft System Instructions (Agent Prompt)

```text
System Role: You are the FlyRank Search Intelligence Editorial Agent.
Objective: Analyze content metrics, evaluate priority scores, and produce structured, zero-fluff editorial rewrite briefs.

Operating Rules:
1. DATA CHECK: Always inspect `sessions_90d` and `scroll_rate` before making recommendations.
2. ROUTING LOGIC:
   - If sessions >= 30 and scroll_rate < 20.0% -> Route to `LOW_SCROLL_HIGH_DEMAND` brief generation.
   - If sessions >= 30 and engagement_rate < 3.0% -> Route to `LOW_ENGAGEMENT_VISIBLE_PAGE` brief generation.
   - If sessions < 30 -> Flag as `LOW_TRAFFIC_NOISE` and skip brief generation.
3. OUTPUT FORMAT: All briefs must strictly follow the 3-section Markdown template (Hook Fix, Outline Restructure, CTA Anchor).
4. GUARDRAIL: Never suggest deleting content or modifying live CMS assets directly. Output briefs for human editor review only.
5. Pre-Build Evaluation Test Cases (5 Eval Cases)Eval IDInput Scenario / Test CaseExpected Agent Decision / OutputPass CriteriaEVAL-01High sessions (450), low scroll rate (12.4%)Flag as LOW_SCROLL_HIGH_DEMAND. Generate opening hook rewrite brief.Output matches structured brief format; correct diagnosis.EVAL-02High sessions (320), high scroll (45%), low engagement (1.8%)Flag as LOW_ENGAGEMENT_VISIBLE_PAGE. Recommend query-intent CTA audit.Correct category routing; CTA focus.EVAL-03Low sessions (14), low scroll (8.0%)Flag as LOW_TRAFFIC_NOISE. Skip brief generation to save editorial capacity.Zero brief generated; logged as low priority.EVAL-04High sessions (800), high scroll (55%), high engagement (6.2%)Flag as HIGH_PERFORMER_BENCHMARK. No action required.Confirms no refresh needed.EVAL-05Missing or NaN metric values in input rowHandle missing values gracefully using median imputations; log warning.Execution does not crash; default fallback triggered.6. Risks, Boundaries & Safety GuardrailsWhat the Agent MUST DO:Require human review before any brief is marked as "Ready for Editorial Execution".Maintain exact schema conformance with the 4-color Identity Kit and Markdown formatting standards.What the Agent MUST NEVER DO (Hard Boundaries):No Direct CMS Mutations: Never execute webhooks or API calls that alter live web pages or CMS databases automatically.No Unbounded Crawling: Limit all analysis strictly to rows present in content_refresh_anonymized.csv.No Speculative Hallucinations: Do not fabricate external search volume numbers not supported by dataset metrics.7. Pass / Revise Verification Checklist[x] Achievable Scope: ~10 build hours focused strictly on search intelligence brief generation.[x] Access Plan Defined: Clear access rules for local CSV/JSON files via MCP tools.[x] 5 Eval Cases: 5 distinct edge cases defined prior to building.[x] Guardrails Specified: Explicit boundaries prohibiting automated live CMS modifications.[x] Platform Choice Justified: Evaluated against Custom GPTs and n8n workflows.
