# Layout and Spacing Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Layout and Spacing"

---

## Start with Too Much White Space

Most interfaces are too cramped. The default instinct to pack content together leads to dense, overwhelming layouts.

**The fix:** Start with more white space than you think you need, then remove it until it looks right. It's much easier to remove space than to add it after the fact.

White space creates breathing room, improves readability, and makes elements feel purposeful. Dense interfaces feel anxious; spacious ones feel confident.

---

## Establish a Spacing and Sizing System

Don't pick spacing values arbitrarily. Define a fixed scale in advance and only use values from that scale.

### A practical spacing scale (base-4 or base-8):

| Token | px value |
|-------|----------|
| 1     | 4px      |
| 2     | 8px      |
| 3     | 12px     |
| 4     | 16px     |
| 5     | 20px     |
| 6     | 24px     |
| 8     | 32px     |
| 10    | 40px     |
| 12    | 48px     |
| 16    | 64px     |
| 20    | 80px     |
| 24    | 96px     |
| 32    | 128px    |
| 40    | 160px    |
| 48    | 192px    |
| 56    | 224px    |
| 64    | 256px    |

**Why it works:** Each step is noticeably different from the next. If two values from the scale look similar, they're wrong — swap one for a value further up or down. This eliminates the "12px or 13px?" debate.

---

## You Don't Have to Fill the Whole Screen

Just because you have space doesn't mean you have to use it. Wide, spacious layouts with constrained content can feel more polished than full-bleed layouts.

### Column width: the problem with fluid grids

Grid-based layouts often make elements wider than they need to be on large screens. A login form stretched to 6 columns may look ridiculous on a 1440px display.

**Use max-widths, not grid fractions, for components that have a natural maximum size.**

```css
/* Don't: */
.login-card { width: 50%; }  /* fluid, grows too large */

/* Do: */
.login-card { max-width: 500px; width: 100%; }  /* caps at a sensible size */
```

**Sidebar widths:** Don't size sidebars as a percentage. Give them a fixed pixel width (e.g., `256px`) that feels right regardless of screen size.

### Multiple column widths in one layout

It's fine to mix width constraints. A "shrink wrap" approach — where containers are only as wide as their content — often looks better than filling all available space.

---

## Grids Are Overrated

12-column grids are a useful tool, but they're not a law. Problems with grid-first thinking:

1. **Column widths are fluid** — the same element can be wider on a medium screen than a large one if you're using column fractions naively
2. **Not everything belongs on a grid** — icons, avatars, and buttons have natural sizes that don't fit grid columns
3. **Don't shrink an element below its ideal size just to fit the grid** — give it a `max-width` and let it shrink only when the screen forces it

**Rule of thumb:** Don't reach for the grid for every layout decision. Use it for large structural divisions (sidebar + content), but let small components size themselves naturally.

---

## Relative Sizing Doesn't Scale

Sizing everything relative to everything else sounds systematic, but it breaks down across different screen sizes.

### The problem

If your body copy is 18px on desktop and your heading is 45px (2.5x ratio), on a small screen you might reduce body to 14px — but that doesn't mean the heading should be 35px. Headings and body copy scale at different rates.

### The fix

- Size elements independently based on what looks good at each breakpoint
- On smaller screens, reduce the contrast between large and small elements — the hierarchy gap should shrink
- Don't apply a uniform scaling factor

**Large headlines on mobile almost always need to shrink more than body text does.** The reverse is also true: very small supporting text often needs to grow a bit on mobile.

---

## Avoid Ambiguous Spacing

When spacing between elements is ambiguous, it's hard to tell which elements are grouped together.

### The principle

Elements should be closer to what they belong to than to what they don't.

**Example:** A form label and its input should have less space between them than between two separate form groups. If the label-to-input gap is the same as the group-to-group gap, the grouping becomes unclear.

### Practical application

- Decrease spacing between related items (label + input, icon + text, heading + first paragraph)
- Increase spacing between unrelated items (between sections, between cards, between independent components)

This is essentially the Gestalt principle of proximity. Use it deliberately to communicate structure without borders or dividers.

---

## Quick Reference: Spacing Heuristics

| Scenario | Approach |
|----------|----------|
| Starting a new layout | Start with too much space, then reduce |
| Component internal padding | Generous — 16px–32px for most cards |
| Label to its input | Tight — 4px–8px |
| Between form groups | More space — 16px–24px |
| Between page sections | Very generous — 48px–96px |
| Content width | Use max-width rather than fluid grid fractions |
| Sidebar width | Fixed px, not a percentage |
| Icon/avatar sizing | Natural size, not grid-aligned |
