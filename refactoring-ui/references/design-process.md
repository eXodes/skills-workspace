# Design Process Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Starting from Scratch"

---

## Start with a Feature, Not a Layout

Don't start by designing the app shell (nav bar, sidebar, logo placement). An app is a collection of features, and you don't have enough information to design navigation until you've designed some features.

**Instead:** Start with a real piece of functionality. Design the actual UI for one feature — for example, "search for a flight" — with the fields and actions it needs.

---

## Detail Comes Later

In early stages, resist making decisions about typefaces, shadows, icons, and colors. These don't matter yet.

**Practical technique:** Design on paper with a thick Sharpie — obsessing over small details becomes impossible.

**Hold color:** Design in grayscale first. You're forced to use spacing, contrast, and size to create hierarchy. This results in a stronger, clearer interface before color is added.

**Don't over-invest:** Sketches and wireframes are disposable. Use them to explore ideas quickly, then leave them behind.

---

## Don't Design Too Much Up Front

You don't need to design every feature before building. Trying to solve every edge case in the abstract (empty states, error states, edge-case data) is setting yourself up for frustration.

**Work in cycles:**
1. Design a simple version of the next feature
2. Build it
3. Encounter real complexity and fix it in the working interface
4. Iterate until no problems remain
5. Return to design mode for the next feature

**Be a pessimist:** Don't include "nice-to-have" functionality in designs you're not ready to build. A comment system without file attachments still ships; a comment system that's blocked waiting for attachments doesn't.

Design the smallest useful version first. Add complexity later.

---

## Choose a Personality

Every design has a personality. Pin it down early — it informs every decision.

### Font Choice
- **Serif typefaces** → elegant, classic, trustworthy (e.g., editorial, financial)
- **Rounded sans-serifs** → playful, friendly, approachable
- **Neutral sans-serifs** → clean, modern, letting other elements carry the personality

### Color Psychology (rough guide)
- **Blue** → safe, familiar, trusted
- **Gold/Yellow** → expensive, sophisticated, premium
- **Pink** → fun, friendly, less serious
- **Green** → natural, healthy, financial (money)
- **Dark/Black** → serious, formal, high-end

Use color psychology as a check, not a formula. Trust your instincts about what "feels right."

### Border Radius
- **No border radius** → formal, serious
- **Small border radius** → neutral, doesn't communicate much on its own
- **Large border radius** → playful, friendly, approachable

Consistency matters: mixing square and rounded corners in the same interface almost always looks worse than sticking to one.

### Language
The words in your UI carry as much personality as the visual design. Formal tone = professional. Casual tone = friendly. Align your copy with your visual personality.

---

## Limit Your Choices

Decision fatigue is real. Unlimited choices (any font size, any color) are paralyzing.

**Solution: Define systems in advance.** Instead of picking from unlimited values, work from a constrained set.

### Systems to define:
- Font sizes (type scale)
- Font weights
- Line heights
- Colors (a palette with defined shades)
- Spacing (margin/padding scale)
- Widths / heights
- Box shadows (elevation scale)
- Border radii
- Border widths
- Opacity values

### How to use a system to decide:
1. Make your best guess (e.g., 16px icon)
2. Compare with the values on either side (12px and 24px)
3. If the middle option looks best, you're done
4. If an outer option looks best, shift your comparison window and repeat

**You don't have to define all systems upfront.** Introduce them as you make decisions — just avoid making the same low-level decision twice.

---

## Designing with Systems (Recurring Theme)

Systems thinking is the core philosophy:
- Don't hand-pick values from a limitless pool
- Build constraints that make later decisions faster and more consistent
- Use process of elimination: constrained options make the right choice obvious

This applies to everything: colors, typography, spacing, shadows, border radii, and more. Later chapters build specific systems for each.
