# 16 — Get Deployment Variables

```text
First, read the project rules from:

./AGENTS.md

Then read the project variables from:

./docs/rebuild/project-variables.md

Follow BOTH strictly.

Use those variables exactly.
Do not guess paths.
If any variable is missing or unclear, stop and report what needs clarification.

If AGENTS.md and project-variables.md conflict:
- AGENTS.md controls behavior/rules.
- project-variables.md controls folder paths and project values.


Analyze this project and define the deployment variables.

Do NOT modify any files.
Do NOT prepare deployment yet.
Do NOT copy or move files.

Your task is ONLY to define the correct deployment variables.

---

Define:

[PROJECT_NAME]
- Use the project name from project-variables.md

[SOURCE_SITE_FOLDER]
- The original website export (read-only)

[REBUILD_SITE_FOLDER]
- The final rebuilt website folder
- This should be the same as [WORKING_SITE_FOLDER]
- This is the source for deployment

[DEPLOY_SITE_FOLDER]
- A new clean folder for deployment output
- Must NOT be the same as [SOURCE_SITE_FOLDER] or [REBUILD_SITE_FOLDER]
- Suggested:
  ./[project-name]-deploy/

[DOCS_FOLDER]
- Use the existing docs folder (usually ./docs/rebuild/)

[NETLIFY_PUBLISH_DIRECTORY]
- If deploying ONLY the deploy folder:
  use "."
- If deploying from parent folder:
  use the folder name (e.g. itext-deploy)

[GITHUB_PAGES_MODE]
- root → if deploy folder will be its own repo
- docs → if deploying from /docs inside a repo

---

Create this file:

[DOCS_FOLDER]/deployment-variables.md

Format EXACTLY like this:

# Deployment Variables

[PROJECT_NAME] = 
[SOURCE_SITE_FOLDER] = 
[REBUILD_SITE_FOLDER] = 
[DEPLOY_SITE_FOLDER] = 
[DOCS_FOLDER] = 
[NETLIFY_PUBLISH_DIRECTORY] = 
[GITHUB_PAGES_MODE] = 

---

## Rules

- [SOURCE_SITE_FOLDER] is read-only
- [REBUILD_SITE_FOLDER] is the final rebuilt site
- Deployment MUST copy from [REBUILD_SITE_FOLDER], not [SOURCE_SITE_FOLDER]
- [DEPLOY_SITE_FOLDER] is the only folder used for deployment
- Do not guess paths in future steps

---

## Notes

- Explain why each folder was chosen
- Mention any uncertainty
- Confirm whether [REBUILD_SITE_FOLDER] is complete and ready for deployment