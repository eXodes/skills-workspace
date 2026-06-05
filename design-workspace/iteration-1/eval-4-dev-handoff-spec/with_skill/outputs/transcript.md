# Eval Transcript: eval-4-dev-handoff-spec (with_skill)

## Execution Steps

### 1. Load Skill

- Read `/Users/exodes/Projects/skills-workspace/design/SKILL.md`
- Skill loaded: `design` — design workflow specialist

### 2. Route to Reference File

- Identified task type from prompt: "generate a dev handoff spec"
- Routing table match: **"generate handoff spec / ready for dev / spec sheet"** → `references/design-handoff.md`
- Loaded `/Users/exodes/Projects/skills-workspace/design/references/design-handoff.md`

### 3. Gather Design Context from Prompt

Extracted from user prompt:

- **Screen:** Order Review (mobile checkout)
- **Header:** "Review your order"
- **Sections:**
  - Scrollable cart item list (image + name + qty + price)
  - Order summary (subtotal, shipping, tax, total)
  - Promo code field
  - Primary CTA button (fixed at bottom)
- **Context:** Going to dev next sprint — final/pixel-ready stage

### 4. Apply Handoff Spec Template

Following `design-handoff.md` output structure:

- Overview (screen purpose, user context)
- Layout (scroll behavior, sticky elements, safe area)
- Design Tokens (colors, typography, spacing, radius, shadow)
- Components table (all UI components with variants and props)
- Detailed component specs (CartItemRow, OrderSummary)
- States and Interactions (promo field: 5 states; CTA: 4 states; back button)
- Responsive Behavior (mobile portrait + landscape)
- Edge Cases (empty cart, long names, large totals, network errors, free shipping, etc.)
- Animation / Motion (with reduce-motion guidance)
- Accessibility Notes (focus order, ARIA labels, contrast, tap targets)
- Implementation Notes (ScrollView vs FlatList, CTA positioning, server-side validation)

### 5. Output Files

- `handoff-spec.md` — Full developer handoff specification

## Skill Contribution

The `design` skill routed to `design-handoff.md`, which provided:

- The required sections for a complete handoff spec
- The principle "Don't assume — if it's not specified, the developer will guess"
- The token-first approach (reference `spacing-md` not `16px`)
- The "show all states" requirement
- The structured output template with tables for tokens, components, states, responsive, edge cases, motion, and a11y

Without the skill, a response might have produced a shorter, less structured document missing states, edge cases, motion specs, or accessibility details.
