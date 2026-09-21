# Portfolio Tech Stack Decision & Architectural Rationale

**Role & Track:** Applied ML Intern — FlyRank Search Intelligence  
**Objective:** Evaluate and select a free, maintainable portfolio hosting stack tailored to present ML case studies, data contracts, prompt logs, and technical code artifacts.

---

## 1. Primary Constraints & Portfolio Requirements

* **Budget Constraint:** $0 (Free hosting, zero maintenance overhead).
* **Developer Skill Level:** Strong Python / ML pipeline experience; comfortable with basic HTML, CSS, Markdown, and Git workflows.
* **Content Presentation Needs:** High-legibility long-form text (3-beat case studies), technical data tables (pandas summaries, metrics), syntax-highlighted code snippets, and cropped execution screenshots.
* **Dynamic Needs:** **None at this stage.** All metrics, evaluation runs, and case studies are static outputs generated from Python notebooks (`w01` to `w04`).

---

## 2. Evaluation of Three Stack Options

### Option 1: Static HTML5 / CSS3 / Markdown + GitHub Pages (Simplest)
* **Build Method:** Pure HTML5 structure, custom utility CSS using the 4-color Identity Kit (`#F8FAFC`, `#0F172A`, `#334155`, `#2563EB`), and raw Markdown files rendered in `/docs`.
* **Hosting:** GitHub Pages (Free native hosting from repo `/docs` folder).
* **Backend Needed:** No.
* **Trade-Off:** Requires manual HTML layout adjustments if pages scale, but offers zero build pipeline errors, instant deploys, and absolute simplicity.

### Option 2: Astro Static Site Generator + Vercel / Netlify (Balanced)
* **Build Method:** Markdown/MDX component architecture compiled into static HTML via Astro build pipeline.
* **Hosting:** Vercel or Cloudflare Pages (Free tier linked via GitHub webhook).
* **Backend Needed:** No.
* **Trade-Off:** Great developer experience for blog-style updates, but introduces Node.js package dependencies (`npm`), build script maintenance, and setup overhead.

### Option 3: Next.js / React + Vercel (Most Powerful)
* **Build Method:** React component framework with static site generation (SSG) and optional API routes.
* **Hosting:** Vercel Free Tier.
* **Backend Needed:** Optional (Node.js serverless functions available).
* **Trade-Off:** Complete overkill for a static case-study portfolio. Adds heavy JS bundle sizes, complex state management, and maintenance risk if dependencies break.

---

## 3. Pressure-Testing & Comparative Matrix

| Criteria | Option 1: Static HTML + GitHub Pages | Option 2: Astro SSG + Vercel | Option 3: Next.js + Vercel |
|---|---|---|---|
| **Cost** | $0 Forever | $0 (Free Tier) | $0 (Free Tier) |
| **Setup & Build Time** | Immediate (0 build config) | Moderate (1-2 hours) | High (3+ hours) |
| **Maintenance Burden** | Zero dependencies to break | Low-Medium (`npm` updates) | High (Framework versions) |
| **Code & Table Legibility** | High (Direct HTML/Markdown control) | High (MDX support) | High (React components) |
| **2-Week Completion Safety** | **100% Guaranteed** | 85% Guaranteed | 50% Risk of configuration traps |

### Pressure-Test Questions:
* **What breaks if I pick Option 1 (Simplest)?** Nothing breaks. Page navigation relies on plain HTML relative links. Modifying shared navigation headers requires manual edits across HTML files, but for a 3-4 page portfolio, this is trivial.
* **What do I maintain if I pick Option 3 (Most Powerful)?** I would have to maintain React dependencies, Node build configurations, and framework updates for a website that serves purely static data tables and text.
* **Can I finish in two weeks?** Option 1 guarantees completion within hours.

---

## 4. The Backend Question

**Answer:** **No, a dynamic backend is not required.**

All data contracts, model ROC-AUC evaluation outputs, and baseline rules are computed offline inside Jupyter notebooks and exported as static JSON/CSV artifacts (`w04_baseline_metrics.json`). Serving these via static HTML/CSS avoids server maintenance, security vulnerabilities, and deployment failures while ensuring 100% uptime.

---

## 5. Final Decision & Written Rationale

### Chosen Stack: Option 1 — Static HTML5 + CSS3 + GitHub Pages

**Why I Chose Option 1:**  
I am building a machine learning portfolio designed to showcase data rigor, target leakage prevention, and rule encoding. My work is best proven through clean typography, legible metrics tables, syntax-highlighted code blocks, and execution screenshots. 

Option 1 allows me to use the exact **Identity Kit** (`Inter`, `JetBrains Mono`, 4-color palette) with zero build overhead. Hosting directly from the `/docs` directory on GitHub Pages means every `git push` instantly deploys the live portfolio without build pipeline failures.

**Why I Rejected Options 2 and 3:**
1. **Rejected Astro (Option 2):** While Astro is excellent for content sites, configuring a Node build environment detracts focus from ML modeling tasks in Weeks 5 and 6.
2. **Rejected Next.js (Option 3):** Full-stack React adds unnecessary complexity for a static portfolio. It introduces maintenance risks without providing any functional benefit for displaying offline ML notebook results.

**Maintainability & Display Quality Verdict:**
* **Can I maintain this?** Yes. There are zero software packages or external APIs to maintain. The site will render identically years from now.
* **Does it show my work well?** Yes. Plain, unencumbered HTML/CSS puts full focus on the ML case studies, data contracts, and proof screenshots without decorative framework clutter.

---

## 6. Pass / Revise Checklist

- [x] **3 Genuine Options Evaluated:** Evaluated Plain Static, Astro SSG, and Next.js.
- [x] **Pressure-Tested Front-Runner:** Identified trade-offs and build risks.
- [x] **Backend Question Addressed:** Confirmed static site architecture is optimal.
- [x] **Maintainability & Display Justified:** Written rationale focused on zero maintenance overhead and high data legibility.
