# Portfolio Visual Identity & Design System

**Principle:** The design exists strictly to make the data legible and the proof unmistakable. Work first, design second.

---

## 1. Color Palette & Typography Contract

### Palette (3-Color Constraint)
* **Background:** Clean Light Off-White (`#F8FAFC`) — Prevents eye fatigue and keeps code readable.
* **Primary Text / High Contrast:** Dark Slate (`#0F172A`) — High legibility for long-form case studies and tables.
* **Accent Color:** Muted Slate Blue (`#2563EB`) — Used sparingly for links, active states, and metric highlights. Zero decorative gradients.

### Typography
* **Prose & Case Studies:** System Sans-Serif (`Inter`, `-apple-system`, `BlinkMacSystemFont`) — Clean, neutral, human-readable prose.
* **Data, Metrics & Code:** Monospace (`JetBrains Mono`, `Fira Code`) — Applied to table values, SQL queries, column names, and model output metrics (`Precision@20`, `ROC-AUC`).

---

## 2. Image Selection Strategy & Judgment Rules

| Image Type | Usage Rule | Decision Rationale |
|---|---|---|
| **Real Notebook Screenshots** | **MANDATORY** | High-resolution, cropped screenshots of execution outputs, confusion matrices, or pandas tables prove real work was executed. |
| **Data Pipelines & Diagrams** | **ALLOWED** | Clean SVG/Mermaid diagrams showing data movement from BigQuery to feature frames. |
| **Generic AI Stock Imagery** | **REJECTED** | Glowing brains, floating binary code, or metallic robot hands destroy credibility and scream amateur filler. |

---

## 3. Visual Asset Inventory for Portfolio Cases

### Case 1: ML Task Framing & Opportunity Scoring (Week 2)
* **Primary Visual:** Cropped code block screenshot showing `target_low_engagement` proxy construction and `Precision@20` metric calculation.
* **Caption:** *"Defining proxy target cutoffs based on 90-day impressions and scroll rate."*

### Case 2: Data Contract & Leakage Trap (Week 3)
* **Primary Visual:** Side-by-side terminal output showing the **Honest ROC-AUC (0.65)** vs the **Leaked ROC-AUC (0.99)** from `w03_data_contract.ipynb`.
* **Caption:** *"Demonstrating target leakage: Synthetic high score vs clean production baseline."*

---

## 4. Design Judgment Comparison (Before / After)

* **Generic AI Choice (Before):**  
  > *Adding a futuristic 3D hero banner with glowing blue neural network nodes and dark cyber aesthetics to make the page look 'AI-powered'.*

* **Edited Intentional Choice (After):**  
  > *Using a stark off-white layout with a crisp, tightly cropped screenshot of a BigQuery SQL table showing actual row counts and availability filters (`IS TRUE`).*
