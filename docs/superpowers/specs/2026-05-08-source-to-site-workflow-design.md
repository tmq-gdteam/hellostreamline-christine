# Source-to-Site Workflow: Design System First

## Overview
This document outlines a complete end-to-end workflow for designing and building a premium, production-ready website directly from raw source materials (e.g., client notes, transcripts, ideas). The process prioritizes a "Design System First" approach, ensuring a robust, scalable architectural foundation is built before any UI components are assembled.

## Process Flow

The workflow is divided into five distinct phases, leveraging specific agentic skills at each step.

### Phase 1: Brand & Theme Inception
**Goal:** Establish the visual identity and core messaging before writing any code.
* **Trigger:** Raw source material (client notes, ideas, rough copy) is provided.
* **Skills Engaged:**
  * `content-brief-extraction`: Analyzes raw text to pull out the core premise, target audience, primary value proposition, and necessary sections.
  * `brand-guidelines` (or `ckm:brand`): Defines the visual identity, mood, tone, and target aesthetic (e.g., minimal, brutalist, glassmorphism).
* **Deliverable:** A foundational "Brand & Content Brief" document that serves as the guiding light for the design and copy.

### Phase 2: Design Token Architecture
**Goal:** Translate the brand identity into strict mathematical rules and code configurations.
* **Trigger:** Approval of the Brand & Content Brief.
* **Skills Engaged:**
  * `color-system`: Generates exact hex codes for primary, secondary, muted, and accent colors.
  * `typography-scale`: Establishes font pairings and a responsive sizing scale.
  * `spacing-system` & `layout-grid`: Defines grid behaviors and standard paddings/margins.
  * `design-token`: Consolidates all visual rules.
* **Deliverable:** A centralized configuration file (e.g., `tailwind.config.ts` or global CSS variables). Once established, no arbitrary or "magic" numbers are allowed in the codebase.

### Phase 3: The Component Factory
**Goal:** Build individual UI elements in strict isolation using only the locked-in tokens.
* **Trigger:** Completion of the design token configuration.
* **Skills Engaged:**
  * `ckm:ui-styling` & `frontend-design`: Build raw UI components (Buttons, Cards, Navbars, Hero Sections) in the specific stack (e.g., React/Tailwind/shadcn).
  * `ui-ux-pro-max`: Reference best-in-class layouts and patterns (glassmorphism, bento grids, etc.).
  * `animation-principles` & `micro-interaction-spec`: Inject premium feel via hover states, click feedback, and entry animations.
* **Deliverable:** A robust, reusable library of UI components that look beautiful and feel alive, independent of the page layout.

### Phase 4: Page Assembly & Content Injection
**Goal:** Stitch the components together to form the actual pages and flow in the content.
* **Trigger:** Completion of the Component Library.
* **Skills Engaged:**
  * `frontend-design`: Create main page layouts (e.g., `index.tsx`) using `layout-grid` tokens.
  * `information-architecture`: Map the extracted content blocks to the appropriate UI components.
* **Process:** Drop components into the layout and inject the raw text/copy extracted during Phase 1.
* **Deliverable:** A fully assembled, functional frontend application populated with strategic copy.

### Phase 5: Responsive Hardening & Deployment
**Goal:** Polish the site for every device and push it live to the world.
* **Trigger:** Fully assembled frontend application.
* **Skills Engaged:**
  * `responsive-design`: Audit the site from mobile to 4K ultrawide viewports, swapping fixed widths for fluid `clamp()` values.
  * `aesthetic-usability`: Conduct a final sweep to ensure the site looks premium and consistent.
  * `deploy-to-vercel`: Push the codebase to Vercel for hosting.
* **Deliverable:** A live, production URL of the premium, design-system-first website.
