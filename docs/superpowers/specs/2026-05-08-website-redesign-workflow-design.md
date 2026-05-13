# Website Redesign Workflow: 10x Growth-Mode & Token-First Approach

## Overview
This document outlines the standard workflow for executing a purely aesthetic and visual redesign of a website from an existing JavaScript framework export (e.g., React, Next.js, Vue). The primary goal is to elevate the product from a safe, "Maintenance Mode" aesthetic into an aggressive "10x Growth Mode" design. This is achieved by combining rigorous psychological strategy with a "Token-First" technical approach, ensuring consistency, scalability, and high conversion.

## Architecture & Strategy
The redesign will be executed in a progressive, 8-phase approach. We begin with a full-site audit to inventory every page and route, define the psychological sequencing and problem statements, proceed through technical cleanup, establish a scalable token system, redesign the global shell, apply an "Urgency Audit" to the anchor page, cascade the design language to all subpages, and finally harden for all viewports.

## Phase 0: Site Audit & Page Inventory
**Goal:** Before touching any code, establish a complete map of the site — every page, route, and shared element — so nothing is redesigned in isolation or left behind.
* **Skills Utilized:** `information-architecture`, `design-debt-audit`
* **Process:**
  1. **Route Enumeration:** List every page/route in the site (e.g., Home, Programs, About, Enroll, Contact, FAQ, Privacy). Include both top-level nav pages and any deeper funnel/utility routes.
  2. **Page Classification:** Assign each page a preliminary tier (Tier 1 Anchor / Tier 2 High-Impact / Tier 3 Utility) based on its role in the conversion funnel and expected traffic.
  3. **Global Shell Identification:** Identify all shared layout elements that appear across pages: navbar, footer, sidebars, modals, banners. These are not tied to any single page and must be redesigned once, applied everywhere.
  4. **Dependency Mapping:** Note any shared components (e.g., cards, hero variants, CTAs) that appear on multiple pages — these get redesigned once and cascade automatically.
* **Deliverable:** A Page Inventory table (route | tier | shared components used | notes) and a Global Shell component list.

## Phase 1: Growth-Mode Strategic Alignment
**Goal:** Define the strategic ambition, psychological sequence, and problem parameters before touching the codebase.
* **Skills Utilized:** `brainstorming`, `ux-writing`, `design-rationale`
* **Process:** 
  1. **The Problem Breakdown:** Conduct the Skill-Gap Analysis and identify Execution Hurdles to synthesize the "Growth-Mode Problem Statement".
  2. **The Goal Blueprint:** Define the three psychological milestones:
     * *Instant Attention (Split-Second):* Establish the pattern interrupt and visual hook.
     * *Sustained Interest (The 3-Second Rule):* Format the core value proposition to prevent bounce during the initial scroll.
     * *Compelling Action (The Conversion):* Design the natural flow toward the next step so it feels like a logical conclusion.
* **Deliverable:** A Strategic Design Brief that serves as the "North Star" for the redesign.

## Phase 2: Audit & Extraction (The Cleanup Phase)
**Goal:** Understand the current state of the exported code and identify all hardcoded, "Maintenance Mode" design values.
* **Skills Utilized:** `design-debt-audit`
* **Process:** 
  1. Scan the exported JSX and CSS files.
  2. Extract all hardcoded colors (hex, rgb), typography sizes, and spacing values.
  3. Consolidate overlapping or near-identical values (e.g., merging three slightly different shades of brand blue into one authoritative hex code).
* **Deliverable:** A documented summary of the baseline styles and the consolidated brand values.

## Phase 3: Tokenization & Brand Preservation
**Goal:** Establish a robust design system configuration that serves as the single source of truth for the redesign.
* **Skills Utilized:** `design-token`, `color-system`, `typography-scale`
* **Process:**
  1. Translate the consolidated brand values from Phase 2 into semantic design tokens (e.g., `primary`, `secondary`, `muted`, `accent`).
  2. Generate a modular typography scale (`text-sm`, `text-base`, `text-lg`) and a spacing scale (`spacing-4`, `spacing-8`).
  3. Inject these tokens into the framework's configuration file (e.g., `tailwind.config.js` or global CSS variables).
* **Deliverable:** A centralized configuration file containing all brand tokens.

## Phase 4: Component Integration & The Urgency Audit
**Goal:** Replace legacy code with the token system and elevate the aesthetic to a 10x standard.
* **Skills Utilized:** `ui-styling`, `frontend-design`, `aesthetic-usability`
* **Process:**
  1. **Global Shell First:** Redesign the navbar and footer before any page-specific work. The shell sets the visual tone for the entire site. Apply the new design tokens to establish hierarchy, spacing, and interaction patterns at the layout level.
  2. Iteratively update JSX components on the Tier 1 anchor page, stripping out rigid inline styles and arbitrary classes.
  3. Apply the new design tokens to structure the components.
  4. **The Urgency Audit (Mandatory Gate):** 
     * *The Relevance Test:* Identify elements that feel too "safe" and redesign them to be aggressive and boundary-pushing.
     * *The 10x Quality Delta:* Apply deep creative effort to the most critical component (e.g., Hero, Conversion flow) to make it 10x better, not 5% better.
     * *The Inspiration Gap:* Inject one unconventional, pattern-interrupting piece of inspiration into the UI before finalizing.
  5. Implement micro-interactions and aesthetic enhancements based on the audit.
* **Deliverable:** Clean, token-driven anchor page (Tier 1) components with a premium, 10x visual feel and a reusable design language for the full site.

## Phase 4b: Subpage Cascade
**Goal:** Propagate the established design language from the anchor page to every remaining page and route in the site, applying the Urgency Audit at tier-appropriate depth.

### Page Priority Tiers
Not every page requires the same depth of redesign effort. Assign each page to a tier using the following criteria before beginning Phase 4b:

| Tier | Label | Description | Urgency Audit Level |
|------|-------|-------------|---------------------|
| 1 | **Anchor** | Primary conversion or landing page (e.g., Home, Pricing) | Full 10x audit — pattern interrupt + inspiration injection |
| 2 | **High-Impact** | Pages with significant traffic or funnel role (e.g., Programs, About, Enroll) | Relevance Test + 10x Quality Delta |
| 3 | **Utility** | Supporting pages with low direct conversion (e.g., Contact, FAQ, Privacy) | Token cleanup + basic polish only |

* **Skills Utilized:** `frontend-design`, `ui-styling`, `ux-writing`
* **Process:**
  1. Pull the page inventory from Phase 0 and assign each page/route to a tier.
  2. For each **Tier 2** page: apply the established tokens, strip legacy styles, run the Relevance Test and 10x Quality Delta from the Urgency Audit. Do NOT re-run the inspiration injection (already set by Tier 1).
  3. For each **Tier 3** page: apply tokens, strip hardcoded styles, ensure typographic and spacing consistency. Polish only — no structural redesign required.
  4. Verify cross-page visual consistency: headings, CTAs, card styles, and spacing should feel cohesive across all tiers.
* **Deliverable:** All pages/routes redesigned at their appropriate tier depth, visually cohesive as a complete site.

## Phase 5: Responsive & Fluid Hardening
**Goal:** Ensure the 10x aesthetic scales flawlessly across all viewports and all pages, eliminating rigid breakpoints that cause layout breaks.
* **Skills Utilized:** `responsive-design`, `layout-grid`, `lovable-responsive-hardening`
* **Process:**
  1. Audit every page (Tier 1 → 3) for horizontal overflow or structural collapse.
  2. Implement fluid typography and spacing utilizing CSS `clamp()` functions — apply globally via tokens, not per-component.
  3. Refactor fixed-width containers into flexible grid/flexbox layouts utilizing viewport-relative sizing or container queries.
  4. Verify that the global shell (navbar, footer) is fully responsive at all breakpoints.
* **Deliverable:** A fully fluid, responsive architecture that supports mobile through 4K viewports across the entire site.

## Phase 6: Quality Assurance & Final Polish
**Goal:** Validate the complete redesign — all pages, all tiers, global shell — against industry standards for accessibility, usability, and strategic goals.
* **Skills Utilized:** `heuristic-evaluation`, `web-design-guidelines`
* **Process:**
  1. Validate that the Tier 1 anchor page achieves all three psychological milestones defined in Phase 1.
  2. Spot-check Tier 2 and Tier 3 pages for token consistency and visual coherence.
  3. Review contrast ratios for all text elements across all pages.
  4. Verify semantic HTML structure, keyboard navigability, and navigation landmarks (especially in the global shell).
  5. Conduct a final cross-page visual pass: does the site feel like a unified product, or do pages feel designed in isolation?
* **Deliverable:** A production-ready, fully redesigned frontend — every page, every viewport.
