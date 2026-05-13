# 17 — Deployment Prep

```text
First, read the project rules from:

./AGENTS.md

Then read the project variables from:

./docs/rebuild/project-variables.md

Then read deployment variables from:

[DOCS_FOLDER]/deployment-variables.md

Follow ALL strictly.

Use variables exactly.
Do not guess paths.
If anything is unclear, stop and report.

If AGENTS.md and variable files conflict:
- AGENTS.md controls behavior
- variable files control paths

---

Prepare the site for GitHub Pages and Netlify deployment.

CRITICAL RULES:

- Do NOT modify [SOURCE_SITE_FOLDER]
- Do NOT modify [REBUILD_SITE_FOLDER] unless fixing deployment issues
- All deployment work happens in [DEPLOY_SITE_FOLDER]
- Keep site as static HTML/CSS/JS
- Do NOT create React/Vite/Next apps
- Do NOT delete files aggressively

---

## Step 1 — Create deploy folder

- If [DEPLOY_SITE_FOLDER] does not exist → create it
- Copy ALL files from:
  [REBUILD_SITE_FOLDER]
  → into:
  [DEPLOY_SITE_FOLDER]

- Ensure:
  [DEPLOY_SITE_FOLDER]/index.html exists

---

## Step 2 — Audit deploy folder

Confirm:
- index.html exists
- css/, js/, images/, fonts/ exist
- site runs as static HTML

---

## Step 3 — Fix internal links

- Check all HTML files inside [DEPLOY_SITE_FOLDER]
- Fix:
  - broken links
  - incorrect relative paths
  - links pointing outside deploy folder
  - links pointing to old designs

- Ensure:
  - navigation works from all pages
  - subfolder links are correct

---

## Step 4 — GitHub Pages prep

Inside [DEPLOY_SITE_FOLDER]:

Create or update:

.nojekyll  
README.md  
.gitignore  

README.md must include:
- project overview
- local preview command
- GitHub Pages deployment steps
- Netlify deployment steps
- note: static HTML/CSS/JS site

.gitignore should exclude:
- .DS_Store
- node_modules/
- .env
- dist/
- build/
- .netlify/

---

## Step 5 — Netlify config

Create inside:

[DEPLOY_SITE_FOLDER]/netlify.toml

Use:

[build]
  publish = "[NETLIFY_PUBLISH_DIRECTORY]"
  command = ""

If deploy folder is repo root:
→ publish = "."

Do NOT add SPA redirects unless confirmed necessary

---

## Step 6 — Local preview

Add to README:

cd [DEPLOY_SITE_FOLDER]
python3 -m http.server 3000

Open:
http://localhost:3000

---

## Step 7 — Deployment report

Create:

[DOCS_FOLDER]/17-deployment-prep-report.md

Include:

- project name
- source folder
- rebuild folder
- deploy folder
- Netlify config
- GitHub mode
- files created
- files changed
- broken links fixed
- unresolved issues
- manual review items

---

## Final checklist

- index.html exists
- all links work
- assets load correctly
- mobile navigation works
- FAQ & Contact use redesigned pages
- README.md exists
- .gitignore exists
- .nojekyll exists
- netlify.toml exists

---

Do NOT deploy yet.
Only prepare and validate.