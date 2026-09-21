# Portfolio Content Map & Through-Line Strategy

**Core Purpose:** Guide visitors from a single high-impact claim to undeniable proof of technical execution, ending with a single direct call to action.

---

## 1. The One-Line Claim

> **"I build machine learning pipelines that turn raw search and user engagement data into prioritized, evidence-backed editorial refresh queues."**

---

## 2. Page Architecture & Content Map

### Page 1: Home & Featured Case Studies (`/index.html`)

* **Section 1: Hero Header**
  * **Content:** One-line claim + short bio + link to GitHub repository.
  * **Visual:** Minimalist monogram (`FR / ML`) with clean typography.
  * **CTA:** *"View Active ML Repositories"* → Points to GitHub.

* **Section 2: Lead Case Study — CTR & Engagement Opportunity Scoring (Week 2 & 3)**
  * **Content:** The 3-Beat case study (Problem, What I Did & Decided, What Came Of It).
  * **Visual:** Cropped screenshot of `w02_ml_task_framing.ipynb` DataFrame and `Precision@20` setup.
  * **CTA:** *"Read Full Case Study & Data Contract"* → Links to Case Deep Dive page.

* **Section 3: Data Contract & Leakage Trap Proof**
  * **Content:** Side-by-side terminal output showcasing honest ROC-AUC vs target leakage detection.
  * **Visual:** High-contrast code snippet from `w03_data_contract.ipynb`.
  * **CTA:** *"Inspect Notebook Code on GitHub"* → Points to `/work/notebooks/w03_data_contract.ipynb`.

* **Section 4: Engineering & Prompt Rigor**
  * **Content:** Highlight of the Prompt Engineering Ladder (5-iteration systematic improvement log).
  * **Visual:** Markdown comparison table from `docs/prompt_ladder.md`.
  * **CTA:** *"View Prompt Iteration Logs"* → Links to `docs/prompt_iteration_log.md`.

---

### Page 2: Case Deep Dive — FlyRank Search Intelligence (`/cases/engagement-scoring.html`)

* **Section 1: Executive Summary & Problem Framing**
  * **Content:** Why fixed rules fail on multi-variable engagement metrics (`scroll_rate` vs `impressions`).
* **Section 2: Data Contract & Feature Frame**
  * **Content:** 5-feature schema and availability justification ("knowable at decision moment").
* **Section 3: The Leakage Trap Experiment**
  * **Content:** Detailed breakdown of how target leakage inflates metrics and how it was resolved.
* **CTA:** *"Explore Full Python Code in Colab / GitHub"* → Direct repo link.

---

### Page 3: About & Contact (`/about.html`)

* **Section 1: Background & Focus**
  * **Content:** ML Intern at FlyRank specializing in search intelligence and structured data contracts.
* **Section 2: Contact & Network**
  * **Primary Action:** Invite technical discussion or portfolio review.
  * **CTA:** *"Reach out on LinkedIn / GitHub"* → Direct profile links.

---

## 3. "Still Need to Gather" Proof List

Items required to complete the portfolio build during upcoming modeling weeks:

1. [ ] **High-Res Screenshots:** Clean, cropped captures of executed Colab cells (`w02` and `w03`).
2. [ ] **Model Evaluation Charts:** Precision-Recall curves and Feature Importance bar charts from upcoming modeling notebooks (Week 4/5).
3. [ ] **Hugging Face Token Connection Proof:** Clean screenshot of successful gated dataset load in Colab via `HF_TOKEN`.
4. [ ] **Live Repository URL:** Final committed `main` branch link for public verification.

---

## 4. Pass / Revise Verification

- [x] **One-line claim:** Single, focused sentence stating the core technical proof.
- [x] **Ordered sections:** Each page has structured sections leading with the strongest work.
- [x] **Aligned CTAs:** All calls to action ladder up to GitHub repository review or direct contact.
- [x] **Honest gather-list:** Remaining pending visual assets explicitly tracked.
