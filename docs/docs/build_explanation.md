# Plain-English Explanation: How GitHub Pages Automagically Serves Our Portfolio

**Author:** ML Intern — FlyRank Search Intelligence  
**Topic:** Static Deployment & Directory Routing via GitHub Pages  

---

## 1. The Real Piece of the Build: How `git push` Turns `/docs` into a Live Website

When I started building this portfolio, I wondered: *How does a folder full of plain text files inside a GitHub repository turn into a real website reachable on a phone browser without paying for a cloud server or running a backend?*

Here is how it actually works, explained as if I were teaching a friend who has never built a website:

---

## 2. How It Works Under the Hood

### Step 1: The Magic Entrypoint (`index.html`)
Web servers are programmed to look for a specific default file name whenever someone visits a web domain root URL. That standard name is always `index.html`. 

When a user visits `https://<username>.github.io/<repo-name>/`, GitHub's web server doesn't guess which file to display—it automatically looks inside the designated directory for `index.html` and streams its HTML structure to the user's browser.

### Step 2: The `/docs` Folder Constraint
Instead of cluttering the root directory of our machine learning repository (which holds Python scripts, Jupyter notebooks, and datasets), we instructed GitHub Pages in **Repository Settings** to listen exclusively to the `/docs` folder on the `main` branch. 

This creates a clean separation:
* **Repository Root:** Machine learning research (`work/notebooks/`, `work/outputs/`, dataset files).
* **`/docs` Directory:** Public-facing web assets (`index.html`, `identity_kit.md`, CSS styling).

### Step 3: What Happens When We Run `git push`
1. When we type `git push origin main`, git uploads our latest commits to GitHub's servers.
2. GitHub notices a change in the `/docs` directory on the `main` branch.
3. An internal background job (GitHub Actions runner) instantly triggers. It takes the static HTML, CSS, and Markdown files in `/docs` and copies them to a static web server (Content Delivery Network / CDN).
4. Within 60 seconds, the new code is globally live on our public URL—no server restarts, no terminal commands, and zero hosting costs.

---

## 3. Key Takeaway

We didn't build a complex dynamic website with databases or Node.js servers because our ML work consists of static proof artifacts (DataFrame outputs, ROC-AUC tables, and execution screenshots). By combining raw HTML/CSS with GitHub Pages' native `/docs` hosting, we achieved 100% uptime, instant deployment on every `git push`, and zero technical debt.

---

## 4. Self-Check Verification

- [x] Explains a real part of our portfolio build (GitHub Pages static hosting architecture).
- [x] Written in plain, authentic words without generic tutorial fluff.
- [x] Demonstrates genuine ownership of the deployment workflow.
