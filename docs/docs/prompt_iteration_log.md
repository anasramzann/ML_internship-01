# Prompt Iteration Log & Cross-Model Comparison

**Track:** FlyRank Applied Search Intelligence  
**Target Task:** Evaluating page-level search & engagement metrics to prioritize content refresh queues.

---

## 1. Naive Version (Baseline / Run 0)

### Prompt
> "Tell me which articles on my website need to be rewritten."

### Output Excerpt
> "To determine which articles need rewriting, you should look at your Google Analytics. Articles with low pageviews, high bounce rates, or outdated information are usually good candidates. You can also update old statistics, fix broken links, or improve headlines."

### Observation Notes
* **What changed in prompt:** Baseline prompt — single-line, ambiguous request.
* **What changed in output:** N/A (Baseline).
* **Observed Output Difference:** Extremely generic advice. It gave textbook SEO definitions instead of analyzing actual data or outputting a actionable list.
* **Failure Point:** No data context, no specific criteria, no actionable structure.

---

## 2. Iteration 1: Role Assignment

### Prompt
> "**You are a Senior Search Intelligence Specialist at FlyRank.** Evaluate website performance data and identify underperforming articles that require an immediate editorial refresh."

### Output Excerpt
> "As a Senior Search Intelligence Specialist, I recommend analyzing page performance across three primary buckets: 1. Traffic Decay (loss in impressions/clicks), 2. Low Engagement (high impressions but low scroll depth), and 3. Content Staleness. Please provide your CSV or page-level metrics so I can extract the specific URLs for your refresh queue."

### Observation Notes
* **Applied Technique:** Role Assignment (System / Persona Framing).
* **Observed Output Difference:** The tone shifted from generic advice to an analytical workflow. The model adopted professional SEO terminology (e.g., "traffic decay", "scroll depth") and explicitly asked for structured data input.
* **Remaining Weakness:** Still conversational; lacks concrete mathematical rules and context about dataset schema.

---

## 3. Iteration 2: Context and Motivation

### Prompt
> "You are a Senior Search Intelligence Specialist at FlyRank. **We are working with `content_refresh_anonymized.csv` containing search and user engagement metrics (90-day impressions, 90-day sessions, scroll rate, engagement rate). Our editorial team has limited bandwidth and can only review 10 pages per week. Our goal is to catch high-exposure pages that fail to engage readers so we don't waste editorial time on zero-traffic pages.** Identify top candidate articles."

### Output Excerpt
> "Understood. Given your constraint of 10 pages per week, we must filter out zero-traffic pages first. We will focus strictly on pages where `sessions_90d >= 30` or `impressions_90d >= 500`. From this high-exposure pool, we will surface pages with `scroll_rate < 20%` or `engagement_rate < 3%` as primary candidates for rewrite."

### Observation Notes
* **Applied Technique:** Context & Business Motivation.
* **Observed Output Difference:** The AI instantly adapted to capacity constraints (10 pages/week limit) and inferred logical cutoff filters (`sessions_90d >= 30`) without being explicitly given the math yet.
* **Remaining Weakness:** Output is still descriptive text rather than a structured data table.

---

## 4. Iteration 3: Few-Shot Examples

### Prompt
> "You are a Senior Search Intelligence Specialist at FlyRank. Analyze search & engagement metrics to identify high-exposure, low-engagement pages for editorial review.
> 
> **Here are two examples of input data and desired classification output:**
> 
> **Input Example 1:** `content_id: c_101`, `impressions_90d: 1200`, `sessions_90d: 85`, `scroll_rate: 14.2%`, `engagement_rate: 1.5%`  
> **Output Example 1:** `c_101` | High Priority | `low_scroll_high_demand` | High impressions (1200) but readers drop off early (14.2% scroll rate).
> 
> **Input Example 2:** `content_id: c_304`, `impressions_90d: 12`, `sessions_90d: 2`, `scroll_rate: 8.0%`, `engagement_rate: 0.5%`  
> **Output Example 2:** `c_304` | Ignore | `low_demand_noise` | Insufficient traffic volume to justify editorial hours.
> 
> Analyze the incoming dataset accordingly."

### Output Excerpt
> "`c_8812` | High Priority | `low_scroll_high_demand` | 512 sessions with 11.0% scroll rate indicate strong demand but poor content retention.  
> `c_0021` | Ignore | `low_demand_noise` | 15 impressions; low volume makes this page low value for rewrite."

### Observation Notes
* **Applied Technique:** Few-Shot Prompting (In-context learning).
* **Observed Output Difference:** The AI flawlessly learned the taxonomy (`low_scroll_high_demand` vs `low_demand_noise`) and stopped flagging low-volume noise pages.
* **Remaining Weakness:** Output format was inconsistent — mixed plain text lines with inline markdown.

---

## 5. Iteration 4: Output Structure Enforcement

### Prompt
> "You are a Senior Search Intelligence Specialist at FlyRank. Analyze search & engagement metrics to identify high-exposure, low-engagement pages.
> 
> [Examples omitted for brevity]
> 
> **Output Requirement:**  
> **Return ONLY a clean Markdown Table. Do NOT include markdown code block wrappers (```), introductory text, or concluding chatter. Use these exact headers:**  
> `| Content ID | Priority Tier | Reason Code | Metrics Summary | Recommended Editorial Action |`"

### Output Excerpt
| Content ID | Priority Tier | Reason Code | Metrics Summary | Recommended Editorial Action |
|---|---|---|---|---|
| `c_8812` | High Priority | `low_scroll_high_demand` | 512 sessions, 11.0% scroll, 1.2% engagement | Rewrite intro hook, restructure headings, and add visual graphics |
| `c_4011` | Medium Priority | `low_engagement_visible_page` | 340 sessions, 19.2% scroll, 2.4% engagement | Update call-to-actions and align content intent with user search query |

### Observation Notes
* **Applied Technique:** Strict Output Formatting.
* **Observed Output Difference:** 100% clean Markdown table. Zero intro chatter ("Here is your table:"), making it directly readable by downstream scripts or automated reporting tools.
* **Remaining Weakness:** The rationale behind priority assignment was implicit rather than systematically reasoned step-by-step.

---

## 6. Iteration 5: Step Decomposition (Chain-of-Thought)

### Prompt
> "You are a Senior Search Intelligence Specialist at FlyRank.
> 
> **Execution Steps:**
> 1. **Filter Volume:** Check if `impressions_90d >= 500` or `sessions_90d >= 30`. If false, classify as `low_demand_noise` and drop.
> 2. **Evaluate Engagement:** For qualified pages, check if `scroll_rate < 20.0%` or `engagement_rate < 3.0%`.
> 3. **Assign Priority:** 
>    - High Priority: Meets Volume filter AND `scroll_rate < 20.0%`.
>    - Medium Priority: Meets Volume filter AND `engagement_rate < 3.0%` (with scroll rate >= 20%).
> 4. **Generate Output:** Format strictly as a Markdown table (Max 10 rows, sorted by sessions descending).
> 
> Output ONLY the table."

### Output Excerpt
| Content ID | Priority Tier | Reason Code | Metrics Summary | Recommended Editorial Action |
|---|---|---|---|---|
| `c_8812` | High Priority | `low_scroll_high_demand` | 512 sessions, 11.0% scroll | Rewrite opening intro; add visual anchors above fold |
| `c_1092` | High Priority | `low_scroll_high_demand` | 410 sessions, 15.4% scroll | Audit mobile layout and sticky navigation elements |
| `c_4011` | Medium Priority | `low_engagement_visible_page` | 340 sessions, 22.1% scroll | Match content intent with search query intent |

### Observation Notes
* **Applied Technique:** Step Decomposition / Chain-of-Thought Guardrails.
* **Observed Output Difference:** Deterministic accuracy. Logical edge cases (e.g. pages with good scroll depth but poor overall engagement rate) were classified into `Medium Priority` exactly as dictated by Step 3 rules.
* **Overall Assessment:** Reached production quality.

---

## 7. Cross-Model Comparison (Claude vs ChatGPT)

The final decomposed prompt (Iteration 5) was executed on both **Claude 3.5 Sonnet** and **ChatGPT (GPT-4o)** using identical data inputs.

| Dimension | Claude (3.5 Sonnet) | ChatGPT (GPT-4o) | Comparison Analysis |
|---|---|---|---|
| **Tone & Style** | Analytical, concise, zero conversational noise. | Slightly more descriptive in editorial action column. | Claude adhered strictly to the negative constraint ("NO chatter"), whereas GPT-4o added slight descriptive fluff inside table cells. |
| **Constraint Adherence** | 100% adherence to Markdown formatting and 10-row cap. | 100% adherence to math rules; added markdown fence wrappers (```markdown) despite negative constraint. | Claude was stricter with raw text formatting requirements. |
| **Logic & Accuracy** | Correctly calculated step logic and priority buckets. | Correctly calculated step logic and priority buckets. | Both models achieved 100% classification accuracy based on the step rules. |
| **Failure Point** | None noted. | Failed negative constraint regarding code block wrappers. | GPT-4o defaulted to wrapped markdown output. |

---

## 8. Final Reusable Prompt Template

```markdown
# Role
You are a Senior Search Intelligence Specialist at FlyRank.

# Task
Analyze page-level search and engagement metrics from `content_refresh_anonymized.csv` and generate a prioritized content refresh queue for non-technical SEO content editors.

# Decision & Filtering Logic
Execute the following logic in order:
1. Volume Gate: Keep only rows where `sessions_90d >= 30` OR `impressions_90d >= 500`. Discard all lower volume rows as noise.
2. High Priority Rule: Flag as `High Priority` with Reason Code `low_scroll_high_demand` if `scroll_rate < 20.0%`.
3. Medium Priority Rule: Flag as `Medium Priority` with Reason Code `low_engagement_visible_page` if `scroll_rate >= 20.0%` AND `engagement_rate < 3.0%`.

# Output Requirements
- Output STRICTLY a Markdown table with exact columns:
  | Content ID | Priority Tier | Reason Code | Metrics Summary | Recommended Editorial Action |
- Limit output to top 10 rows sorted by `sessions_90d` descending.
- DO NOT output introductory text, concluding summaries, or markdown fence block wrappers.
