# Section Background Fix Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Fix the abrupt background color changes across the `deploy/index.html` page by localizing the page-wide background gradient into the hero section and using a solid white background for the body.

**Architecture:** We will update `deploy/css/growth-mode-overrides.css` by changing the `--bg-primary` token to `#fff` and creating a new `--bg-hero` token containing the gradient. We will then apply `--bg-hero` specifically to the `.hero` element.

**Tech Stack:** CSS, HTML

---

### Task 1: Update CSS Tokens

**Files:**
- Modify: `deploy/css/growth-mode-overrides.css:20`

- [ ] **Step 1: Update the `--bg-primary` variable and add `--bg-hero`**

```css
  /* Semantic Mappings */
  --bg-primary: #fff;
  --bg-hero: linear-gradient(180deg, #fff8f6 0%, #fff 25%, #faf7ff 65%, #fff 100%);
```

- [ ] **Step 2: Commit**

```bash
git add deploy/css/growth-mode-overrides.css
git commit -m "style: update semantic mapping tokens for background fix"
```

---

### Task 2: Apply Hero Background

**Files:**
- Modify: `deploy/css/growth-mode-overrides.css:60` (or add to Global Shell Normalization section)

- [ ] **Step 1: Add the `.hero` specific background override**

Add the following CSS rules to explicitly apply the hero gradient:
```css
/* Apply hero gradient specific to hero section */
body.growth-mode .hero {
  background: var(--bg-hero);
}
```

- [ ] **Step 2: Verify in browser**

Run: `npm run dev` (if a local server is needed) or refresh the browser.
Expected: The background is solidly white from the `.logos` section downward, and the gradient only applies to the `.hero` container. The `.pricing` and `.roi` sections should retain their localized gradients correctly.

- [ ] **Step 3: Commit**

```bash
git add deploy/css/growth-mode-overrides.css
git commit -m "style: apply hero background gradient"
```
