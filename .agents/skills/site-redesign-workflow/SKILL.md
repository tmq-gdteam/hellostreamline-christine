---
name: site-redesign-workflow
description: Use when redesigning an existing website or codebase that needs to shift from a legacy aesthetic to a high-conversion, Growth-Mode design, or when refactoring hardcoded styles into a fluid token system
---

# Site Redesign Workflow

## Overview
A strict, subagent-driven framework for executing a full-site visual redesign of an existing website. This workflow shifts a project from a safe "Maintenance Mode" into a "10x Growth Mode" aesthetic by combining psychological strategy (Milestones) with a Token-First technical approach — applied to every page, every viewport, not just the hero.

## When to Use
Use this whenever you need to refactor or redesign an existing messy codebase, upgrade a legacy site to a high-conversion Growth-Mode aesthetic, standardize arbitrary styling into semantic design tokens, or apply responsive hardening across all pages.

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

### Phase 1: Growth-Mode Strategic Alignment (The Engine)
**Goal:** Define the strategic ambition and psychological sequence before touching code, acting as an elite Silicon Valley strategist.
**Action:** Dispatch a subagent to synthesize the Strategy.
**Skills Required:** `@[/brainstorming]`, `@[/ux-writing]`, `@[/growth-mode-design]`
**Instruction:** "Adopt the persona of a Top 5 Silicon Valley Designer. If `artifacts/design-director-brief.md` exists from a previous step, bypass strategy generation and use it as your foundational blueprint. Otherwise, analyze the source material and output `artifacts/growth-mode-blueprint.md` defining the Goal Blueprint (Instant Attention, Sustained Interest, Compelling Action) for the Tier 1 anchor page."

⛔ **MANDATORY STOPPING POINT 1: Strategy Review**
You MUST halt and present the `artifacts/growth-mode-blueprint.md` to the user. Do not touch the codebase until this artifact is approved.

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
**Instruction:** "Read `artifacts/brand-values-audit.md` (or `artifacts/design-director-brief.md`). Translate these values into semantic tokens (primary, secondary, muted, accent, text-base). **Tone Preservation Constraint:** You must strictly follow the Light/Dark mode polarity specified in the brief. Do not automatically default to dark theme tokens unless explicitly instructed. Generate a modular typography scale and a spacing scale. Inject into `tailwind.config.js` or global CSS variables."

⛔ **MANDATORY STOPPING POINT 3: Token Architecture Review**
You MUST halt and show the updated configuration file. Ensure the user confirms the semantic token naming represents their brand before touching components.

---

### Phase 4: Global Shell + Anchor Page (The Urgency Audit)
**Goal:** Redesign the global shell first, then the Tier 1 anchor page at 10x quality. The shell defines the visual tone for every page — it is not optional.
**Action:** Dispatch a subagent for shell redesign, then a second for the anchor page Urgency Audit.
**Skills Required:** `@[/ui-styling]`, `@[/frontend-design]`, `@[/growth-mode-design]`

**Step 1 — Global Shell:**
**Instruction:** "Redesign the navbar and footer using the new design tokens. **CRITICAL: You must copy the exact literal HTML DOM structure of the legacy navbar and footer. Do NOT recreate them from scratch.** Apply the new design tokens by targeting the existing legacy classes (e.g., Webflow classes) via CSS overrides. The shell must reflect the 10x Growth-Mode visual language before any page work begins."

**Step 2 — Anchor Page Urgency Audit (Reference-Driven):**
**Instruction:** "For the Tier 1 anchor page, the Design Reference layout becomes the new structural foundation. **CRITICAL: Apply the Architecture Preservation Rule for the Global Shell: You MUST retain the literal HTML DOM blocks of the legacy navbar and footer.** For the page body, use the Design Reference's layout and structure as the design direction. Migrate and rewrite the legacy content to fit this new layout using an AI copywriter to improve the messaging if needed. Execute the full Urgency Audit against `artifacts/growth-mode-blueprint.md`: (1) Relevance Test, (2) 10x Quality Delta, (3) Inspiration Gap."

⛔ **MANDATORY STOPPING POINT 4: Shell + Anchor Page Review**
You MUST halt and have the user review the navbar, footer, and anchor page (via localhost or screenshots). Verify the shell is site-ready and the anchor page hits the 10x Growth-Mode standard — not just a clean maintenance standard.

---

### Phase 4b: Subpage Cascade
**Goal:** Propagate the design language from the anchor page to every remaining route at the appropriate tier depth.

**Page Priority Tiers (assign in Phase 0):**

| Tier | Label | Urgency Audit Level |
|------|-------|---------------------|
| 1 | **Anchor** | Full 10x — pattern interrupt + inspiration injection (done in Phase 4) |
| 2 | **High-Impact** | Relevance Test + 10x Quality Delta only (no inspiration re-injection) |
| 3 | **Utility** | Token cleanup + typographic/spacing consistency. Polish only. |

**Action:** Dispatch one subagent per Tier 2 page (or group Tier 3 pages into a single pass).
**Skills Required:** `@[/frontend-design]`, `@[/ui-styling]`, `@[/ux-writing]`
**Instruction (Tier 2):** "For [page name]: use the new Anchor Page as your design direction and pattern library. Apply design tokens and strip legacy styles. Run the Relevance Test and 10x Quality Delta from the Urgency Audit. **CRITICAL: Apply the Architecture Preservation Rule for the Global Shell. You must retain the literal HTML DOM blocks of the legacy navbar and footer.** For the subpage body, adapt the layout to match the new Anchor Page's aesthetic, rewriting or improving the content as needed to fit the new premium design."
**Instruction (Tier 3):** "For [page names]: apply tokens, strip hardcoded styles, ensure typographic and spacing consistency. Polish only — no structural redesign."

⛔ **MANDATORY STOPPING POINT 4b: Subpage Coherence Review**
You MUST halt and present completed subpages to the user. Verify headings, CTAs, card styles, and spacing feel cohesive across all tiers — the site should feel like a unified product, not isolated pages.

---

### Phase 5: Responsive & Fluid Hardening
**Goal:** Make the architecture fluid from mobile to 4K — across every page, not just the hero.
**Action:** Dispatch a subagent to refactor layout containers site-wide.
**Skills Required:** `@[/responsive-design]`, `@[/layout-grid]`, `@[/lovable-responsive-hardening]`
**Instruction:** "Audit every page (Tier 1 → 3) for horizontal overflow or structural collapse. Implement `clamp()` fluid typography and spacing — apply globally via tokens, not per-component. Refactor fixed-width containers into flexible grid/flexbox with viewport-relative sizing or container queries. Verify the global shell (navbar, footer) is fully responsive at all breakpoints."

⛔ **MANDATORY STOPPING POINT 5: Layout Review**
You MUST halt and request the user to test the UI across viewports on multiple pages, including the global shell.

---

### Phase 6: Quality Assurance & Final Polish
**Goal:** Validate the complete redesign — all pages, all tiers, global shell — against industry standards.
**Action:** Dispatch a subagent for final heuristic review.
**Skills Required:** `@[/heuristic-evaluation]`, `@[/web-design-guidelines]`
**Instruction:** "Validate the Tier 1 anchor page achieves all three psychological milestones from Phase 1. Spot-check Tier 2 and Tier 3 pages for token consistency and visual coherence. Review contrast ratios across all pages. Verify semantic HTML, keyboard navigability, and navigation landmarks in the global shell. Conduct a final cross-page visual pass: does the site feel like a unified product or do pages feel designed in isolation? Provide a QA report."

✅ **FINAL COMPLETION POINT: QA Sign-off**
Present the QA report to the user and confirm the codebase is production-ready — every page, every viewport.

---

## Red Flags - STOP and Start Over
- "I'll just clean up the JSX classes inline right away" → No. Stop. Phase 0, 1 & 2 must happen first.
- "We don't need a strategy brief, the design is obvious" → No. You must complete Phase 1 Strategic Alignment. Obvious designs lead to "Maintenance Mode".
- "I made it clean and accessible, that's a 10x improvement" → Clean is 5%. You must run the Urgency Audit (Phase 4) to hit 10x.
- "The codebase is small, I'll do tokenization and component updates together" → No. Blending phases creates spaghetti code.
- "I'll redesign the hero and we're done" → No. Every page needs to be touched. Run Phase 4b for all Tier 2 and Tier 3 pages.
- "I'll simplify the navigation or remove copy to make it cleaner" → No. Apply the Architecture Preservation Rule. Never delete text or routes, only change the aesthetics.
- "I applied dark mode because it looks more premium" → No. Apply the Tone Preservation Constraint. Never override the Light/Dark mode polarity specified in the brief.
- "The subpages don't need the Urgency Audit, they're utility pages" → Tier 3 still needs token cleanup. "No audit" ≠ "no work".
- "I'll do the global shell last after all the pages are done" → No. The global shell MUST be done first in Phase 4. It defines the visual language every page inherits.

## Rationalization Table

| Excuse | Reality |
|--------|---------|
| "The client didn't provide enough context for the psychological sequence." | Then ask clarifying questions. Do not skip Phase 1. |
| "A clean Tailwind conversion is enough." | A clean UI is "Maintenance Mode." The Urgency Audit ensures it is "Growth Mode." |
| "I'll do the Urgency Audit at the very end during QA." | You cannot audit what is already finalized. The Urgency Audit must happen during Phase 4. |
| "We only need to redesign the homepage." | Phase 0 exists to prevent this. Every page gets covered at its tier-appropriate depth. |
| "The subpages will look fine once the tokens are applied." | Token application ≠ redesign. Tier 2 pages need the Relevance Test and Quality Delta, not just a class swap. |
| "The navbar is fine as-is, I'll focus on components." | The global shell is the visual foundation. Skipping it makes every page feel inconsistent. |
| "Phase 4b can be one big subagent pass." | Dispatch one subagent per Tier 2 page to maintain isolation and focus. Tier 3 pages may be grouped. |

## Common Mistakes
- **Skipping Phase 0:** Starting without a page inventory means subpages get forgotten until QA — then it's too late.
- **Skipping Phase 1:** Diving straight into technical cleanup without defining the psychological hooks.
- **Applying magic numbers:** If you encounter a new value needed in Phase 4, you MUST update the token configuration in Phase 3 first.
- **Hero-only mentality:** Applying full 10x effort only to the hero and leaving all other pages at "Maintenance Mode" quality.
- **Global shell last:** Redesigning all pages first and bolting on the navbar/footer at the end causes visual inconsistency.

## Implementation Details
Always use `@[/subagent-driven-development]` to isolate each phase. Do NOT attempt to run all 8 phases in a single subagent prompt. For Phase 4b, dispatch one focused subagent per Tier 2 page to maintain quality and reviewability.
