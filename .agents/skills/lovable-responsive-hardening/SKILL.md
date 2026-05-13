---
name: lovable-responsive-hardening
description: Use when you need to automate responsive hardening of exported Lovable codebases, replacing rigid pixel constraints and breakpoints with fluid primitives like clamp() and container queries.
---

# Lovable Responsive Hardening Workflow

## Overview
A standalone, reusable skill to automate the responsive hardening of exported Lovable codebases. It systematically replaces rigid pixel constraints and breakpoint-heavy Tailwind classes with fluid primitives, ensuring the UI scales seamlessly from mobile to 4K ultrawide monitors without layout breakage.

## When to Use
Use this whenever you receive a raw export from Lovable (or a similarly generated codebase) that looks great on one viewport but suffers from horizontal overflow, tiny 4K typography, or rigid breakpoints on other devices.

## Core Pattern

This workflow executes in 5 sequential phases. **You MUST STOP and request user review at the designated gates before proceeding.** Violating the sequence guarantees a fragile layout and regressions.

### Phase 1: Vulnerability & Pixel Audit
**Goal:** Identify rigid constraints that will break on mobile or look tiny on 4K monitors.
**Action:** Dispatch a subagent to scan the Lovable export for fixed pixel widths (`w-[800px]`, `max-w-7xl`), rigid margin/padding steps (`md:p-8 lg:p-16`), and fixed typography (`text-4xl md:text-6xl`).
**Skills Required:** `@[/design-debt-audit]`
**Instruction:** "Audit the target codebase for all hardcoded, non-fluid styling rules and output an audit report detailing the vulnerabilities."

⛔ **MANDATORY STOPPING POINT 1: Audit Review**
You MUST halt and present the audit report of the rigid classes found before touching any code. Wait for user approval to proceed.

### Phase 2: Fluid Configuration Injection
**Goal:** Equip the codebase with the necessary fluid primitives.
**Action:** Dispatch a subagent to update configuration files.
**Skills Required:** `@[/ckm:ui-styling]`, `@[/design-token]`
**Instruction:** "Update `tailwind.config.ts` (or equivalent) to support fluid utilities. Add `@tailwindcss/container-queries`, and inject global utility variables (like `clamp()` definitions) into `index.css`."

### Phase 3: Container & Grid Fluidity
**Goal:** Replace rigid Tailwind breakpoint layouts with fluid wrappers scaling cleanly to ultrawide.
**Action:** Dispatch a subagent to refactor outer layout bounds.
**Skills Required:** `@[/layout-grid]`, `@[/responsive-design]`
**Instruction:** "Remove rigid center constraints (`max-w-7xl mx-auto`). Replace with a dynamic viewport-relative pattern (`w-[92%] lg:w-[86vw] xl:w-[70vw] max-w-[2200px] mx-auto`). Update internal flex/grids using `@container` queries or `minmax` to prevent horizontal overflow."

### Phase 4: Typography & Spacing Conversion
**Goal:** Make text and whitespace scale infinitely without breakpoint "snapping".
**Action:** Dispatch a subagent to refactor typography and spacing classes.
**Skills Required:** `@[/typography-scale]`, `@[/spacing-system]`
**Instruction:** "Strip stacked text breakpoints (`text-xl md:text-3xl`). Replace with CSS `clamp()` functions (`text-[clamp(1.5rem,4vw,3rem)]`). Apply `text-balance` to headings and `text-pretty` to body paragraphs."

⛔ **MANDATORY STOPPING POINT 2: Visual Scaling Review**
You MUST halt and require the user to visually review the typography scaling and layout boundaries (e.g., via localhost) before proceeding to final QA.

### Phase 5: Mobile Edge-Case & QA Hardening
**Goal:** Ensure zero horizontal scroll bars and seamless touch interaction on mobile devices.
**Action:** Dispatch a subagent to execute a final defensive pass.
**Skills Required:** `@[/web-design-guidelines]`, `@[/accessibility-audit]`
**Instruction:** "Apply `overflow-x-hidden` on the `body`. Ensure all touch targets meet the `44px` minimum. Wrap complex elements (data tables, large images) in `overflow-x-auto` to allow internal scrolling."

✅ **FINAL COMPLETION POINT: QA Sign-off**
Present a final QA checklist confirming verification across mobile, tablet, 1080p, and 4K viewports, handing the responsive codebase back to the user.

## Red Flags - STOP and Start Over
- "I'll just add another breakpoint `xl:text-7xl`" -> No. Stop. Replace with `clamp()` (Phase 4).
- "I'll skip the audit because Lovable exports are usually standard" -> No. Run Phase 1. You cannot fix what you haven't audited.
- "I'll do Phase 3 and 4 at the same time" -> No. Container fluidity must be solved before internal typography is scaled.

## Common Mistakes
- **Ignoring Container Queries:** Relying solely on viewport units (`vw`) for internal grid elements instead of `@container` queries (`cqw`). Use container queries for component-level fluidity.
- **Skipping Touch Targets:** Neglecting to increase padding on mobile buttons, leading to failed QA.

## Implementation Details
Use `@[/subagent-driven-development]` for parallelization across components in Phases 3 and 4 where appropriate, but strictly enforce the review gates.
