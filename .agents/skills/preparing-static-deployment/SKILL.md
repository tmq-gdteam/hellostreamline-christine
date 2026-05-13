---
name: preparing-static-deployment
description: Use when preparing a statically built or exported website for deployment to GitHub Pages or Netlify, separating build output from deployment artifacts.
---

# Preparing Static Deployment

## Overview
Enforces a strict boundary between working files and deployment artifacts to ensure clean, static deployments to GitHub Pages or Netlify without corrupting source code.

## When to Use
- User asks to "deploy the site", "push this live", or "get the export ready for GitHub Pages"
- Preparing static HTML/CSS/JS for hosting
- **When NOT to use:** When deploying a modern app framework with its own automated build pipeline (use `deploy-to-vercel` instead).

## The Iron Law of Deployment
**Never deploy working folders. Never modify working files to fix deployment paths.**

## Quick Reference / Core Workflow

1. **Isolate:** Copy `[REBUILD_FOLDER]` to a new `[DEPLOY_FOLDER]`.
2. **Cleanup:** Remove any development or host-specific folders that were copied over (e.g., delete `.netlify/`, `.git/`, or `node_modules/` from inside `[DEPLOY_FOLDER]`).
3. **Fix Links:** Fix broken paths and relative links **ONLY** inside `[DEPLOY_FOLDER]`.
4. **GitHub Pages Prep:** Create `.nojekyll` (mandatory), `.gitignore`, and `README.md` inside `[DEPLOY_FOLDER]`. **CRITICAL:** Create `.github/workflows/deploy.yml` with a standard GitHub Pages deployment action. Without this, the "Pages" link will not show up in the GitHub UI and the site will not automatically deploy from the main branch.
5. **Netlify Config (Optional):** ONLY if deploying to Netlify, add `netlify.toml` with `publish = "."`. Skip if deploying exclusively to GitHub Pages.
6. **Verify:** Run `python3 -m http.server 3000` locally in `[DEPLOY_FOLDER]` before pushing.

## Common Rationalizations & Red Flags

If you find yourself thinking any of these, **STOP. Delete your work and start over.**

| Excuse | Reality |
|--------|---------|
| "I'll just deploy the rebuild folder since we're out of time." | Mixing working files with deployment artifacts causes leaked source files and broken paths. Use a clean boundary. |
| "I'll fix the links directly in the rebuild folder." | The rebuild folder is for development. The deploy folder is where relative pathing is finalized for the live domain. |
| "We don't need a .nojekyll file." | GitHub Pages ignores folders starting with underscores (e.g., `_assets`) by default unless `.nojekyll` exists. Your CSS/JS will 404. |
| "I'll run npm run build to get it ready." | If it's an exported static site, it doesn't need a JS bundler. Treat it as static HTML. |
| "We don't need a GitHub Actions workflow, GitHub Pages does it automatically." | GitHub Pages does not automatically trigger from `main` without manual Settings configuration (which may be blocked/hidden). A `.github/workflows/deploy.yml` guarantees the "Pages" link appears and deploys successfully. |

## Red Flags - STOP and Start Over
- Deploying directly from `./source` or `./rebuild`
- Modifying non-deploy folders to fix deployment issues
- Skipping the `.nojekyll` file
- Skipping the `.github/workflows/deploy.yml` file for GitHub Pages

**All of these mean: Delete the deployment attempt. Create a clean deploy folder.**
