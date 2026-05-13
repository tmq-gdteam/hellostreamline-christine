---
name: chatgpt-redesign-workflow
description: Use when executing a visual redesign based on a ChatGPT-generated reference index and a Design Director brief, specifically when the old architecture must be preserved but the aesthetic completely overhauled.
---

# ChatGPT Redesign Workflow

## Overview
A strict, subagent-driven framework for executing a full-site visual redesign using a ChatGPT-generated reference `index.html` and a `design-director-brief.md`. This workflow mirrors the structure of the standard site redesign workflow but shifts the design execution to rely heavily on the ChatGPT reference file.

This workflow enforces the **Architecture Preservation Rule**: the target site's original navigation links and footer MUST be retained (DOM structure intact) while the page bodies are overhauled to match the ChatGPT reference design. It also mandates full Subpage automation, Mobile Responsiveness, and AEO/SEO/GEO optimization.

## When to Use
- You have received a `design-director-brief.md` from the `chatgpt-design-director` skill.
- You are provided with a ChatGPT reference `index.html` that serves as the new aesthetic target.
- The existing site needs a design overhaul but must keep its original nav links and footer routing.

## Core Pattern

This workflow executes in **8 sequential phases**. **You MUST STOP and request user review at the designated gates before proceeding.** Violating the sequence or skipping gates guarantees a generic, low-impact result and pages left behind.

---

### Phase 0: Site Audit & Page Inventory
**Goal:** Map every page, route, and shared element before touching any code. Nothing gets redesigned in isolation or forgotten.
**Action:** Dispatch a subagent to enumerate the full site.
**Skills Required:** `@[/information-architecture]`, `@[/design-debt-audit]`
**Instruction:** "List every route in the site. Assign each a preliminary tier: Tier 1 (Anchor — primary conversion/landing page), Tier 2 (High-Impact — funnel/traffic pages like Programs, About, Enroll), or Tier 3 (Utility — low-conversion pages like Contact, FAQ, Privacy). Identify all shared layout elements (navbar, footer, sidebars, modals). Map shared components that appear on multiple pages. Output a Page Inventory table (route | tier | shared components | notes) and a Global Shell component list to `artifacts/page-inventory.md`."

⛔ **MANDATORY STOPPING POINT 0: Site Scope Review**
You MUST halt and present `artifacts/page-inventory.md` to the user. Confirm tier assignments and the global shell list before any strategy work begins.

---

### Phase 1: Strategic Alignment (Brief Consumption)
**Goal:** Ingest the design constraints before touching code.
**Action:** Dispatch a subagent to synthesize the Strategy.
**Skills Required:** `@[/brainstorming]`, `@[/ux-writing]`
**Instruction:** "Read `artifacts/design-director-brief.md`. This brief is the ultimate source of truth for tokens, tone, and direction. If the ChatGPT reference contradicts the brief (e.g., reference is dark mode but brief specified light mode), the brief wins."

⛔ **MANDATORY STOPPING POINT 1: Strategy Review**
You MUST halt and verify the brief is understood. Do not touch the codebase until this is approved.

---

### Phase 2: Audit & Extraction (The Cleanup Phase)
**Goal:** Identify hardcoded design values in the legacy code.
**Action:** Dispatch a subagent to scan the codebase.
**Skills Required:** `@[/design-debt-audit]`
**Instruction:** "Scan the exported JSX and CSS files. Extract all hardcoded colors, typography sizes, and spacing. Consolidate overlapping values into an authoritative list. Output to `artifacts/brand-values-audit.md`."

⛔ **MANDATORY STOPPING POINT 2: Brand Baseline Review**
You MUST halt and present the audit to the user. Do not build tokens until they approve the consolidated foundation.

---

### Phase 3: Tokenization & Brand Preservation
**Goal:** Establish a single source of truth configuration.
**Action:** Dispatch a subagent to build the design system constraints.
**Skills Required:** `@[/design-token]`, `@[/color-system]`, `@[/typography-scale]`
**Instruction:** "Read `artifacts/brand-values-audit.md` and `artifacts/design-director-brief.md`. Translate these values into semantic tokens (primary, secondary, muted, accent, text-base). **Tone Preservation Constraint:** You must strictly follow the Light/Dark mode polarity specified in the brief. Generate a modular typography scale and a spacing scale. Inject into `tailwind.config.js` or global CSS variables."

⛔ **MANDATORY STOPPING POINT 3: Token Architecture Review**
You MUST halt and show the updated configuration file. 

---

### Phase 4: Global Shell + Reference-Driven Anchor Page
**Goal:** Redesign the global shell first, then the Tier 1 anchor page heavily relying on the ChatGPT reference `index.html`.
**Action:** Dispatch a subagent for shell redesign, then a second for the anchor page.
**Skills Required:** `@[/ui-styling]`, `@[/frontend-design]`

**Step 1 — Global Shell:**
**Instruction:** "Redesign the navbar and footer using the new design tokens. **CRITICAL: You must copy the EXACT literal HTML DOM structure of the legacy navbar and footer.** DO NOT recreate them from scratch using the ChatGPT reference nav/footer. Apply the new design tokens by targeting the existing legacy classes via CSS overrides."

**Step 2 — Reference-Driven Anchor Page:**
**Instruction:** "For the Tier 1 anchor page body, use the layout, design, and styling found in the ChatGPT reference `index.html`. **CRITICAL: Apply the Architecture Preservation Rule for the Global Shell: You MUST retain the literal HTML DOM blocks of the legacy navbar and footer.** Migrate the target site's content into the ChatGPT reference's structural patterns. DO NOT completely overwrite the actual content and information architecture with placeholder text from ChatGPT."

⛔ **MANDATORY STOPPING POINT 4: Shell + Anchor Page Review**
You MUST halt and have the user review the navbar, footer, and anchor page.

---

### Phase 4b: Subpage Cascade
**Goal:** Propagate the ChatGPT reference design language from the anchor page to every remaining route, automating all subpages.
**Action:** Dispatch one subagent per Tier 2 page (or group Tier 3 pages into a single pass).
**Skills Required:** `@[/frontend-design]`, `@[/ui-styling]`, `@[/ux-writing]`

**Instruction (Tier 2 & 3):** "For [page name]: use the new Anchor Page (based on the ChatGPT reference) as your pattern library. Apply design tokens and strip legacy styles. **CRITICAL: Apply the Architecture Preservation Rule for the Global Shell. You must retain the literal HTML DOM blocks of the legacy navbar and footer.** For the subpage body, adapt the layout to match the new Anchor Page's premium aesthetic, rewriting or improving the content as needed."

⛔ **MANDATORY STOPPING POINT 4b: Subpage Coherence Review**
You MUST halt and present completed subpages to the user.

---

### Phase 5: Responsive Hardening & AEO/SEO/GEO Optimization
**Goal:** Ensure perfect mobile responsiveness and comprehensive search/answer engine optimizations.
**Action:** Dispatch a subagent to refactor layout containers and inject metadata site-wide.
**Skills Required:** `@[/responsive-design]`, `@[/layout-grid]`, `@[/lovable-responsive-hardening]`

**Instruction:** "Audit every page (Tier 1 → 3). 
1. **Responsive Hardening:** Implement `clamp()` fluid typography and spacing. Refactor fixed-width containers into flexible grid/flexbox with viewport-relative sizing or container queries. Verify the global shell (navbar, footer) is fully responsive at all breakpoints.
2. **AEO, SEO, and GEO Optimization:** Inject semantic HTML tags (`<article>`, `<section>`, `<aside>`). Add robust structured data (JSON-LD Schema). Optimize meta tags, Open Graph tags, alt attributes, and heading hierarchy (`h1` → `h6`) for Search Engine Optimization (SEO), Answer Engine Optimization (AEO), and Generative Engine Optimization (GEO)."

⛔ **MANDATORY STOPPING POINT 5: Layout & Optimization Review**
You MUST halt and request the user to test the UI viewports and verify metadata.

---

### Phase 6: Quality Assurance & Final Polish
**Goal:** Validate the complete redesign against the brief and reference index.
**Action:** Dispatch a subagent for final heuristic review.
**Skills Required:** `@[/heuristic-evaluation]`, `@[/web-design-guidelines]`
**Instruction:** "Validate the Tier 1 anchor page accurately reflects the ChatGPT reference index styling and the design director brief. Review contrast ratios. Verify semantic HTML, keyboard navigability. Provide a QA report."

✅ **FINAL COMPLETION POINT: QA Sign-off**

---

## Red Flags - STOP and Start Over
- "The legacy navbar has messy classes, it's easier to use the reference navbar." → Easier means breaking the site's routing. You MUST preserve the target DOM and apply CSS overrides.
- "The ChatGPT reference is perfect, I'll just copy the whole file." → You are overwriting the actual content and information architecture of the real site. Content must be mapped.
- "I'll do the global shell last" → No. The global shell MUST be done first in Phase 4.
- "I'll redesign the hero and we're done" → No. Every page needs to be touched. Run Phase 4b for all Tier 2 and Tier 3 pages.

**All of these mean: Revert the code. Start over.**
