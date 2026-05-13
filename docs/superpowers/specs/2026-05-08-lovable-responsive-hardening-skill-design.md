# Lovable Responsive Hardening Skill Design

## Overview
A standalone, reusable skill to automate the responsive hardening of exported Lovable codebases. The workflow systematically replaces rigid pixel constraints and breakpoint-heavy Tailwind classes with fluid primitives (CSS `clamp()`, container queries, dynamic viewport widths), ensuring the UI scales seamlessly from mobile screens to 4K ultrawide monitors.

## Workflow Phases

### Phase 1: Vulnerability & Pixel Audit
**Goal:** Identify rigid constraints that will break on mobile or look tiny on 4K monitors.
* **Agent Action:** The agent scans the Lovable export for fixed pixel widths (e.g., `w-[800px]`, `max-w-7xl`), rigid margin/padding steps (`md:p-8 lg:p-16`), and fixed typography (`text-4xl md:text-6xl`).
* **Gate:** 🛑 **STOP AND REVIEW:** The agent presents an audit report of the rigid classes found before touching code.

### Phase 2: Fluid Configuration Injection
**Goal:** Equip the codebase with the necessary fluid primitives.
* **Agent Action:** The agent updates `tailwind.config.ts` (or equivalent) to support fluid utilities. This includes adding standard container utilities, injecting `@tailwindcss/container-queries`, and setting up a global `index.css` with `clamp()` utility variables if needed.

### Phase 3: Container & Grid Fluidity
**Goal:** Replace rigid Tailwind breakpoint layouts with fluid wrappers that scale cleanly to ultrawide.
* **Agent Action:** The agent refactors the outer bounds of the site. It removes rigid center constraints (like `max-w-7xl mx-auto`) and replaces them with a dynamic viewport-relative pattern (e.g., `w-[92%] lg:w-[86vw] xl:w-[70vw] max-w-[2200px] mx-auto`). Internal flex/grids are updated to use container queries (`@container` and `@sm:`) or `minmax` to prevent horizontal overflow and awkward wrapping on intermediate devices.

### Phase 4: Typography & Spacing Conversion
**Goal:** Make text and whitespace scale infinitely without breakpoint "snapping".
* **Agent Action:** The agent strips stacked text breakpoints like `text-xl md:text-3xl lg:text-5xl` and replaces them with CSS `clamp()` functions (e.g., `text-[clamp(1.5rem,4vw,3rem)]`). It also applies `text-balance` to headings to prevent orphans, and `text-pretty` to body paragraphs for optimal line lengths across changing viewport widths.
* **Gate:** 🛑 **STOP AND REVIEW:** The agent halts and requires the user to visually review the typography scaling and layout boundaries (via localhost) before doing final QA.

### Phase 5: Mobile Edge-Case & QA Hardening
**Goal:** Ensure zero horizontal scroll bars and seamless touch interaction on mobile devices.
* **Agent Action:** The agent executes a final defensive pass. It ensures the body/main-wrapper is protected against horizontal overflow (`overflow-x-hidden` on `body` as a fallback). It audits touch targets to ensure they meet the `44px` minimum size for mobile usability. Finally, it ensures complex UI elements (like data tables, large imagery, or Lovable-generated widgets) are wrapped in `overflow-x-auto` to allow horizontal scrolling within their containers rather than breaking the page width.
* **Gate:** ✅ **FINAL COMPLETION:** The agent presents a final QA checklist confirming verification across mobile, tablet, 1080p, and 4K viewports, and officially hands the responsive codebase back to the user.

## Implementation Details
The skill will instruct the agent executing it to use `@[/subagent-driven-development]` for parallelization where appropriate, but strictly enforce the review gates. The final outcome is a fluid, modern, production-ready codebase without the rigidity common to automated exports.
