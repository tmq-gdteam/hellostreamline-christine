---
name: hero-to-full-site-cascade
description: Use when a site has an approved, redesigned hero section but the remaining sections of the anchor page and all subpages have not been updated to match the Growth-Mode design language
---

# Hero to Full-Site Cascade

## Overview
A focused, subagent-driven workflow for completing a full-site redesign when the hero section (Tier 1 anchor) is already approved. It cascades the established design language — tokens, visual patterns, psychological milestones — to every remaining section of the anchor page, the global shell, all subpages, and every viewport.

**Entry condition:** The hero section is approved. Tokens exist. A Growth-Mode Blueprint exists (or can be extracted from the hero).

**Do NOT use this skill if:** No hero or tokens exist yet. Use `site-redesign-workflow` instead to start from scratch.

## When to Use

- Hero section is done and approved by the user ✅
- Token configuration (`tailwind.config.js` or CSS variables) is already established ✅
- Remaining anchor page sections (Features, Testimonials, CTA, Footer, etc.) are still legacy ❌
- Global shell (navbar, footer) has not been redesigned ❌
- Subpages (About, Programs, Enroll, Contact, FAQ, etc.) are untouched or still Maintenance-Mode ❌

**NOT for:**
- Starting a redesign from scratch (use `site-redesign-workflow`)
- Responsive hardening only on an already-complete site (use `lovable-responsive-hardening`)

---

## Page Priority Tiers

Before running any phase, classify every route. Reference `artifacts/page-inventory.md` if it exists; otherwise create it now.

| Tier | Label | Description | Urgency Audit Level |
|------|-------|-------------|---------------------|
| 1 | **Anchor** | Primary conversion or landing page — hero already done | Remaining sections only: Relevance Test + 10x Quality Delta |
| 2 | **High-Impact** | Traffic/funnel pages (Programs, About, Enroll) | Relevance Test + 10x Quality Delta |
| 3 | **Utility** | Low-conversion pages (Contact, FAQ, Privacy) | Token cleanup + typographic consistency only |

> The Inspiration Gap (unconventional pattern interrupt) was already injected in the approved hero. Do NOT re-inject it on Tier 2 or 3 pages. The hero sets the visual language; subpages inherit it.

---

## Core Pattern

This workflow executes in **5 sequential phases**. **You MUST STOP at each gate before proceeding.** Skipping gates breaks the cascade — subpages will drift from the hero's design language.

---

### Pre-Flight: Extract the Established Design Language
**Goal:** Read what already exists before writing a single line of code.
**Action:** Dispatch a subagent to extract the current state.
**Instruction:** "Read the following and produce `artifacts/cascade-baseline.md`: (1) The existing token configuration file (`tailwind.config.js` or global CSS variables). (2) The approved hero component code — extract its visual patterns (color use, spacing rhythm, typographic hierarchy, component shapes, micro-interaction style). (3) The Growth-Mode Blueprint at `artifacts/growth-mode-blueprint.md` if it exists. If it does not exist, synthesize one from the hero's visual decisions. Output: token inventory, hero visual pattern summary, and psychological milestone map (Instant Attention achieved ✅, Sustained Interest target, Compelling Action target)."

⛔ **MANDATORY STOPPING POINT 0: Baseline Confirmation**
Present `artifacts/cascade-baseline.md` to the user. Confirm the extracted design language accurately reflects the approved hero before any new work begins.

---

### Phase 1: Page Inventory & Shell Audit
**Goal:** Map every remaining route and verify whether the global shell (navbar, footer) has been redesigned yet.
**Action:** Dispatch a subagent to enumerate and classify.
**Skills Required:** `@[/information-architecture]`
**Instruction:** "List every route in the site that is NOT the hero/anchor page. Assign each a tier (Tier 2: High-Impact / Tier 3: Utility). Inspect the current navbar and footer: do they use the new design tokens and match the Growth-Mode visual language established in the hero? Output a Page Inventory table to `artifacts/page-inventory.md` (route | tier | shell status: redesigned/legacy | shared components | notes)."

⛔ **MANDATORY STOPPING POINT 1: Scope Review**
Present `artifacts/page-inventory.md`. Confirm the tier assignments and whether the shell needs redesign. Do not begin component work until the user approves the scope.

---

### Phase 2: Remaining Anchor Page Sections + Global Shell
**Goal:** Complete the anchor page below the hero and establish the global shell site-wide.

**Step 1 — Global Shell (if not already redesigned):**
**Action:** Dispatch a subagent.
**Skills Required:** `@[/ui-styling]`, `@[/frontend-design]`
**Instruction:** "Using the token configuration and the visual patterns in `artifacts/cascade-baseline.md`, redesign the navbar and footer. The shell must: use the established design tokens, reflect the Growth-Mode visual tone (not a legacy or generic style), establish clear navigation hierarchy and interaction states. Do NOT introduce new visual concepts — inherit from the hero."

**Step 2 — Remaining Anchor Page Sections:**
**Action:** Dispatch a subagent per section group (e.g., Features block, Testimonials, CTA strip).
**Skills Required:** `@[/ui-styling]`, `@[/frontend-design]`, `@[/growth-mode-design]`
**Instruction:** "For [section name] on the anchor page: strip legacy inline styles and arbitrary classes. Apply design tokens. Run the Relevance Test: does this section feel too 'safe' relative to the hero? Run the 10x Quality Delta: apply deep effort to make it match the hero's quality level. Do NOT run the Inspiration Gap injection — that pattern is already set. Implement micro-interactions consistent with the hero's motion style."

⛔ **MANDATORY STOPPING POINT 2: Anchor Page Completeness Review**
Present the completed anchor page and updated shell. Verify the page reads as a unified, cohesive Growth-Mode experience from hero to footer — not a mix of old and new sections.

---

### Phase 3: Subpage Cascade
**Goal:** Propagate the design language to every Tier 2 and Tier 3 page.
**Action:** Dispatch one subagent per Tier 2 page; batch Tier 3 pages together.
**Skills Required:** `@[/frontend-design]`, `@[/ui-styling]`, `@[/ux-writing]`

**Instruction (Tier 2 — one subagent per page):**
"For [page name]: apply design tokens from the configuration file. Strip all legacy hardcoded styles. Run the Relevance Test: which elements feel too 'safe' or generic? Redesign them aggressively. Run the 10x Quality Delta: elevate the most important component on this page. DO NOT re-run the Inspiration Gap injection — inherit the visual language from the anchor page hero. Ensure headings, CTAs, card styles, and spacing are consistent with the anchor page."

**Instruction (Tier 3 — batch):**
"For [list of utility page names]: apply design tokens, strip hardcoded styles, ensure typographic scale and spacing consistency match the anchor page. Polish only — no structural redesign. Verify contrast ratios for all text elements."

⛔ **MANDATORY STOPPING POINT 3: Subpage Coherence Review**
Present all redesigned subpages. Ask: do these pages feel like they belong to the same site as the hero? Verify headings, CTAs, card styles, and spacing are cohesive across all tiers before hardening.

---

### Phase 4: Responsive & Fluid Hardening (All Pages)
**Goal:** Ensure the design scales flawlessly from mobile to 4K — across the anchor page, all subpages, and the global shell.
**Action:** Dispatch a subagent for a site-wide responsive pass.
**Skills Required:** `@[/responsive-design]`, `@[/layout-grid]`, `@[/lovable-responsive-hardening]`
**Instruction:** "Audit every page (Tier 1 remaining sections, Tier 2, Tier 3, global shell) for horizontal overflow or structural collapse. Apply `clamp()` fluid typography and spacing globally via tokens — not per-component. Refactor fixed-width containers into flexible grid/flexbox with viewport-relative sizing or container queries. Verify the navbar and footer are fully responsive at all breakpoints. The hero section is exempt from restructuring — preserve it as-is, only fix overflow if present."

⛔ **MANDATORY STOPPING POINT 4: Cross-Viewport Review**
Request the user to test the UI across mobile, tablet, and desktop on multiple pages including at least one Tier 2 and one Tier 3 page.

---

### Phase 5: Quality Assurance & Final Polish
**Goal:** Validate that the full site is a unified, coherent, production-ready Growth-Mode product.
**Action:** Dispatch a subagent for a final heuristic review.
**Skills Required:** `@[/heuristic-evaluation]`, `@[/web-design-guidelines]`
**Instruction:** "Validate the complete anchor page (hero + remaining sections) achieves all three psychological milestones: Instant Attention (hero ✅), Sustained Interest (below-fold sections), Compelling Action (CTA and conversion flow). Spot-check Tier 2 and Tier 3 pages for token consistency and visual coherence. Review contrast ratios across all pages. Verify semantic HTML, keyboard navigability, and navigation landmarks in the global shell. Final cross-page visual pass: does the entire site feel like a unified Growth-Mode product, or do pages feel designed at different times? Output a QA report."

✅ **FINAL COMPLETION POINT: QA Sign-off**
Present the QA report. Confirm the codebase is production-ready — every section, every page, every viewport.

---

## Red Flags - STOP and Start Over
- "The subpages will look fine once tokens are applied, I don't need to run the Relevance Test" → No. Token application is Tier 3 work. Tier 2 pages require the Relevance Test and 10x Quality Delta.
- "The hero is great, the rest of the site doesn't need to match it" → No. The entire site must feel cohesive. The hero sets the bar — every page is measured against it.
- "I'll skip the shell and go straight to subpages" → No. The global shell (navbar, footer) redesigns first. Every page inherits its visual tone from the shell.
- "I'll redesign all subpages in one big subagent pass" → No. Dispatch one subagent per Tier 2 page. Batching Tier 2 produces generic, unfocused output.
- "The remaining anchor sections don't need as much effort as the hero" → No. The Relevance Test and 10x Quality Delta apply to every remaining section. The hero created expectations — every section must meet them.
- "We can do responsive hardening as we go, not at the end" → No. Run Phase 4 as a dedicated site-wide pass after all redesign work is complete.

## Rationalization Table

| Excuse | Reality |
|--------|---------|
| "The tokens are set, that's enough for the subpages." | Tokens prevent inconsistency. They don't produce Growth-Mode quality. Run the Urgency Audit at the right tier depth. |
| "The client approved the hero so the design language is clear." | Clear to you ≠ applied correctly to all pages. Verify with the Pre-Flight baseline extraction. |
| "Utility pages are just text, they don't need design work." | Tier 3 pages still need token cleanup, typographic consistency, and contrast ratio compliance. |
| "I'll check coherence at QA." | QA is too late to catch structural drift. The Subpage Coherence Review gate (Phase 3) exists for this. |
| "The navbar is fine as-is." | "Fine" is Maintenance Mode. The shell must reflect the Growth-Mode visual language established in the hero. |

## Common Mistakes
- **Skipping the Pre-Flight:** Jumping into components without reading what tokens and patterns already exist leads to conflicts with the approved hero.
- **Inspiration Gap re-injection on subpages:** The hero's pattern interrupt is the unconventional element for the whole site. Adding another one on a subpage creates visual noise, not quality.
- **Magic numbers in subpages:** Any new value added during Phase 3 must go into the token configuration first. Never hardcode a value directly into a component.
- **Leaving the shell for last:** Redesigning all pages before the navbar/footer creates a mismatch — every page will need touch-ups after the shell is done.

## Implementation Details
Always use `@[/subagent-driven-development]` to isolate each phase. Do NOT attempt to run all phases in a single subagent prompt. The Pre-Flight extraction is mandatory even if you believe you know the token system — agents drift without an explicit baseline anchor.
