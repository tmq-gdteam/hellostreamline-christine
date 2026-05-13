---
name: source-to-site-workflow
description: Use when building a new website, landing page, or frontend application from raw source material, client notes, or extraction briefs
---

# Source-to-Site Design Workflow

## Overview
A strict, subagent-driven automation framework for designing and building premium, production-ready websites directly from raw source materials. This enforces a "Design System First" architecture to prevent spaghetti code and inconsistent styling.

## When to Use
Use this whenever starting a completely new web project, page, or feature from unformatted ideas, notes, or copy documents.

## Core Pattern

This workflow executes in 5 sequential phases. **You MUST STOP and request user review at the designated gates before proceeding.** Violating the sequence or skipping gates guarantees architectural failure.

### Phase 1: Brand & Theme Inception
**Goal:** Extract structured brand data from raw inputs.
**Action:** Dispatch a subagent to process the user's raw source material (which will be provided when this skill is triggered).
**Skills Required:** `@[/content-brief-extraction]`, `@[/brand-guidelines]` (or `@[/ckm:brand]`)
**Instruction:** "Extract core premise, audience, value props, and content structure into `artifacts/brand-and-content-brief.md`."

⛔ **MANDATORY STOPPING POINT 1: Brand & Content Strategy Review**
You MUST halt and present `artifacts/brand-and-content-brief.md` to the user. Do not proceed until they approve the strategy.

### Phase 2: Design Token Architecture
**Goal:** Translate brand into strict mathematical rules.
**Action:** Dispatch a subagent to generate configuration.
**Skills Required:** `@[/color-system]`, `@[/typography-scale]`, `@[/spacing-system]`, `@[/layout-grid]`, `@[/design-token]`
**Instruction:** "Use the approved brief to generate hex codes, typography scales, and spacing rules. Inject them directly into `tailwind.config.ts` or global CSS."

⛔ **MANDATORY STOPPING POINT 2: Token Architecture Sign-off**
You MUST halt and show the generated tokens. Do not build components until the user approves the constraints.

### Phase 3: The Component Factory
**Goal:** Build reusable UI elements in isolation.
**Action:** Dispatch a subagent to build the components.
**Skills Required:** `@[/ckm:ui-styling]`, `@[/frontend-design]`, `@[/ui-ux-pro-max]`, `@[/animation-principles]`, `@[/micro-interaction-spec]`
**Instruction:** "Using ONLY the established design tokens, build isolated components (Buttons, Cards, Navbars, Hero Sections). Inject hover states and entry animations."

⛔ **MANDATORY STOPPING POINT 3: Component Library Review**
You MUST halt and have the user verify the aesthetic polish and interactions.

### Phase 4: Page Assembly & Content Injection
**Goal:** Assemble the layout and inject the raw copy.
**Action:** Dispatch a subagent to build the pages.
**Skills Required:** `@[/frontend-design]`, `@[/information-architecture]`
**Instruction:** "Assemble `index.tsx` using layout tokens. Drop in the built components and inject the text from the Phase 1 extraction."

⛔ **MANDATORY STOPPING POINT 4: Assembly & Flow Review**
You MUST halt and present the assembled layout for narrative review.

### Phase 5: Responsive Hardening & Deployment
**Goal:** Polish for all devices and deploy.
**Action:** Dispatch a subagent for final QA and deployment.
**Skills Required:** `@[/responsive-design]`, `@[/aesthetic-usability]`, `@[/deploy-to-vercel]`
**Instruction:** "Audit across all viewports. Swap fixed widths for `clamp()`. Perform final aesthetic pass. Deploy to Vercel."

✅ **FINAL COMPLETION POINT**
Present the live Vercel URL to the user.

## Red Flags - STOP and Start Over
- "I can just use a random hex code this one time" -> No. Add it to tokens or start over.
- "I'll do the content extraction and token generation in one step to save time" -> No. Stop at Gate 1.
- "The components look fine, I won't bother the user with a review" -> No. Halt and wait for sign-off.

## Common Mistakes
- **Skipping Phase 2 (Tokens)**: Attempting to style components without a centralized `tailwind.config.ts` leads to inconsistent "magic numbers."
- **Skipping Review Gates**: Assuming the user will like the brand brief or tokens without asking.
- **Blending Phases**: Assembling pages while still defining tokens. This causes immediate technical debt.

## Implementation Details
Always use `@[/subagent-driven-development]` to isolate each phase. Do NOT attempt to run all 5 phases in a single subagent prompt.
