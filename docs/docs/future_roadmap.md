# Portfolio Evolution Plan: Maintenance & Next Case Study Roadmap

**Author:** ML Engineering Intern — FlyRank Search Intelligence  
**Document:** Post-Graduation Portfolio Protocol & Expansion Plan  
**Target File for Expansion:** `docs/index.html` & `docs/case_studies/`

---

## 1. The 3-Beat Case Study Addition Playbook

To add a new project in under 30 minutes without re-architecting the portfolio, follow this standardized 3-beat structure:

### Where It Lives:
- **Primary Page:** Add a new row to the `Verified Build Artifacts` list in `docs/index.html`.
- **Detail Page:** Create `docs/case_studies/cs_02_[project_name].md` using the template below.

### The 3-Beat Structure:
1. **Beat 1: The Problem (The Bottleneck & Risk)**  
   - *Formula:* State the specific operational friction, baseline metric, and what was at risk.  
   - *Example:* "Manual intent audits took 15 hours/week per editor, missing 40% of queries that drifted semantically from target content."
2. **Beat 2: What I Did (The Method & Validation)**  
   - *Formula:* Detail the data volume, feature engineering/model architecture, and leak-free validation split.  
   - *Example:* "Built a sentence-transformer embedding classifier evaluating 120k query-page pairs using temporal holdout splits."
3. **Beat 3: What Came of It (The ROI & Proof Receipts)**  
   - *Formula:* State the performance lift vs baseline, human-in-the-loop limits, and link to executed notebook/JSON receipts.  
   - *Example:* "Achieved 0.91 Cosine Intent Match accuracy, reduced manual audit time by 70%, and exported validated JSON briefs."

---

## 2. Named Next Project & Concrete Calendar Reminder

* **Next Project Title:** *Semantic Search Query Intent Drift Analyzer & Vector Embedding RAG Pipeline*
* **Core Objective:** Detect when top-ranking organic keywords shift in user intent relative to an article’s heading hierarchy using vector embeddings (`all-MiniLM-L6-v2`) and cosine distance alerts.

### Concrete Reminder Evidence:
- [x] **Calendar Nudge Set:** Google Calendar / Apple Reminders event scheduled.
- **Event Name:** `[FlyRank Portfolio] Add Case Study #2 (Query Intent Drift)`
- **Scheduled Date:** November 1, 2026 at 10:00 AM PKT
- **Recurrence:** Bi-monthly review on the 1st of every second month.

---

## 3. AI Project Context Preservation

To ensure future case studies require a 15-minute conversation rather than a full system rebuild:

- **Saved Project Setup:** The dedicated Claude / AI Assistant Project workspace contains the repo's full system prompt, styling guidelines, WCAG accessibility rules, and HTML structure.
- **Identity Kit Retained:** Monogram tags (`FR / ML TRACK`), dark theme palette (`#0F172A`, `#1E293B`, `#2563EB`), and non-defensive voice guidelines are locked in the workspace instructions.
- **Fast Update Prompt:**  
  > *"Load my FlyRank portfolio stack context. I have a new executed notebook `work/notebooks/w11_semantic_drift.ipynb`. Generate Beat 1, Beat 2, and Beat 3 markdown blocks matching my existing `docs/index.html` format."*

---

## 4. Maintenance Checklist

- [x] 3-beat addition framework documented.
- [x] Next project scope named (`Semantic Search Query Intent Drift Analyzer`).
- [x] Concrete reminder set for recurring portfolio maintenance.
- [x] AI Assistant workspace context preserved for low-cost future updates.
