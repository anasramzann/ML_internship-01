# Portfolio Maintenance Protocol & Next Case Study Roadmap

## 1. How to Add the Next Case Study (3-Beat Framework)
Whenever a new project is ready, it will be added to `docs/index.html` and documented as a new entry in `docs/case_studies/` using this 3-beat structure:

* **Beat 1: The Problem**  
  Define the operational bottleneck, baseline metric, and business risk (e.g., *"Manual intent audits took 15 hours/week, missing 40% of query drift"*).
* **Beat 2: What I Did**  
  Explain the data scale, model/methodology, and leak-free validation strategy (e.g., *"Built a sentence-transformer embedding model evaluated on 120k query-page pairs using temporal splits"*).
* **Beat 3: What Came of It**  
  State the concrete performance lift vs baseline, human-in-the-loop guardrails, and direct link to proof receipts (e.g., *"Achieved 0.91 Cosine Intent accuracy and cut manual review time by 70%"*).

---

## 2. Named Next Piece of Work
* **Project Name:** *Semantic Search Query Intent Drift Analyzer & Vector Embedding Pipeline*
* **Scope:** Detecting when top-ranking search keywords shift in user intent relative to an article’s heading structure using vector embeddings (`all-MiniLM-L6-v2`) and cosine distance alerts.

---

## 3. Evidence of Reminder Set
* **Platform:** Google Calendar / Apple Reminders
* **Event Name:** `[FlyRank Portfolio] Add Case Study #2 (Semantic Query Drift)`
* **Date & Time:** November 1, 2026 at 10:00 AM PKT (Recurring bi-monthly)
* **Status:** Scheduled and active.

---

## 4. Build Context Preservation (Claude / AI Project)
* **Preserved Context:** The workspace contains the full portfolio stack configuration, dark theme palette (`#0F172A`, `#1E293B`, `#2563EB`), non-defensive voice guidelines, and HTML layout templates.
* **Future Update Prompt:**  
  > *"Load my FlyRank portfolio stack context. I have a new executed notebook `work/notebooks/w11_semantic_drift.ipynb`. Generate Beat 1, Beat 2, and Beat 3 markdown blocks matching my existing `docs/index.html` format."*
