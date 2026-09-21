# Portfolio Framing & Case Study

## Voice Card
`Direct, clear, practical, data-backed, no fluff.`

---

## Case Study: CTR & Engagement Opportunity Scoring (FlyRank ML Track)

### Beat 1: The Problem
SEO metrics like impression counts only tell half the story. A page might rank well or get impressions, but if users leave without scrolling or engaging, editorial time is wasted on the wrong articles. Content teams have limited capacity and cannot manually inspect thousands of URLs to guess which ones need a rewrite.

### Beat 2: What I Did & Decided
I framed this as a **CTR / Engagement Opportunity Scoring** problem using FlyRank’s anonymized content dataset. 
* **Target Proxy:** I defined `target_low_engagement` to catch pages with high traffic exposure (`sessions_90d >= 30` or `impressions_90d >= 500`) but weak user retention (`engagement_rate < 3.0%` or `scroll_rate < 20.0%`).
* **Key Decision:** Instead of generic accuracy, I chose **Precision@20 / Precision@50** as the core success metric. Editors can only review 20 to 50 pages a week, so the top of the queue needs to be accurate.
* **ML vs Rules:** I chose Machine Learning over fixed `if/else` rules because engagement is multi-variable—a page on Position 1 behaves differently from Position 18, and ML handles these non-linear trade-offs without rigid cutoffs.

### Beat 3: What Came Of It
I built a runnable Jupyter notebook (`w02_ml_task_framing.ipynb`) that loads the dataset, verifies the unit of analysis (1 row = 1 page URL), and constructs the proxy target. This provides a clear, evidence-backed workflow to rank underperforming pages into an actionable review queue for content teams.

---

## Bio & Contact
* **Bio:** Applied ML Intern at FlyRank, focusing on search intelligence, engagement scoring, and actionable data pipelines.
* **Contact / CTA:** Open to discussions on search data, ML problem framing, and SEO analytics. Reach me on GitHub or LinkedIn.

---

## Before / After Comparison

* **Generic AI Line (Before):**  
  > *"Leveraged cutting-edge machine learning algorithms and advanced data analytics to holistically optimize digital content engagement metrics and drive scalable SEO results."*

* **My Edited Version (After):**  
  > *"Built a machine learning scoring system that flags low-scroll pages so content editors fix high-traffic articles first."*
