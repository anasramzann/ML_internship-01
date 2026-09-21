# Plain-English Explainer: How Our Portfolio's Single Dynamic Feature Works

**Author:** ML Intern — FlyRank Search Intelligence  
**Feature Built:** Serverless Contact & Editorial Refresh Request Form  
**Provider / Hosting Tier:** Netlify Forms (Free Tier / $0)  

---

## 1. What is a "Backend" in Plain English?

When you look at a static website (HTML, CSS, Markdown), everything you see runs entirely inside the user's browser (the **Frontend** or "Client"). A static page cannot process user inputs, save data to a database, or send emails on its own because it has no memory or server running behind the scenes.

A **Backend** is a web server or database running elsewhere on the internet. It works behind the curtain to take data sent from the browser, process it, securely store it, or route it to other services (like sending an automated email or triggering a machine learning pipeline).

---

## 2. Our Single Dynamic Feature: Serverless Contact Form

Instead of paying $20/month for a full dedicated server or writing Node.js/Python backend code, we wired a **Serverless Form Endpoint** using Netlify Forms.

### How the Data Flows (Step-by-Step):
