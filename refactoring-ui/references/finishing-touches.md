# Finishing Touches Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Finishing Touches" and "Leveling Up"

---

## Supercharge the Defaults

Plain HTML elements — unordered lists, horizontal rules, blockquotes, tables — use browser defaults that are functional but visually bland. Small changes make them look intentional and polished.

### Lists

Replace bullet dots with custom icons or decorative symbols:

```css
/* Use a checkmark icon or brand-colored bullet */
ul.feature-list li::before {
  content: '✓';
  color: var(--primary-500);
  font-weight: bold;
  margin-right: 0.5em;
}
```

Or use a colored number/counter for ordered lists.

### Horizontal rules

A full-width grey line (`<hr>`) rarely looks good. Alternatives:
- Center a short rule: `width: 80px; border-color: var(--primary-500);`
- Decorative separator: use three dots (· · ·), a small icon, or a gradient fade
- Replace the rule with extra vertical spacing alone

### Blockquotes

Add a large quotation mark, a thick left border in your brand color, or a background fill:

```css
blockquote {
  border-left: 4px solid var(--primary-500);
  padding-left: 1.5rem;
  color: var(--grey-600);
  font-style: italic;
}
```

### Tables

Default table borders look dated. Improve with:
- Zebra striping (alternating row backgrounds)
- Horizontal-only dividers (no vertical borders)
- Sticky header with subtle shadow
- Right-align number columns for scannability

---

## Add Color with Accent Borders

A solid block of color can look heavy. A thin accent border or stripe achieves the same "brand color is present" effect without dominating.

**Techniques:**

1. **Top border on cards**
```css
.card {
  border-top: 4px solid var(--primary-500);
  border-radius: 4px;
  background: white;
}
```

2. **Left border on alert/notification bars**
```css
.alert {
  border-left: 4px solid var(--warning-400);
  background: var(--warning-50);
  padding: 1rem 1.5rem;
}
```

3. **Active state indicator for navigation**
```css
.nav-item.active {
  border-bottom: 2px solid var(--primary-500);  /* tab-style */
}
/* or */
.nav-item.active {
  border-left: 3px solid var(--primary-500);   /* sidebar-style */
}
```

These feel more refined than filling the whole element with a brand color.

---

## Decorate Your Backgrounds

Plain white or grey backgrounds can make a UI feel bare. Subtle decoration adds visual interest without distracting from content.

### Options (ordered by subtlety)

1. **Slightly off-white or tinted background** — `background: hsl(220, 30%, 98%)` instead of pure white
2. **Subtle pattern** — dot grid, diagonal lines, or a faint geometric pattern at low opacity
3. **Gradient background** — a very subtle gradient from one grey to another, or from white to a tinted grey
4. **Geometric shapes** — large, low-opacity geometric shapes (circles, abstract blobs) anchored to corners
5. **Repeating SVG pattern** — small icons or motifs that relate to the product's domain

**Key rule:** Decorative backgrounds should be subtle enough that they read as "texture," not as "graphic design element." If you notice the pattern before you notice the content, it's too heavy.

---

## Don't Overlook Empty States

Empty states are the first thing new users see. A blank page with no content and no guidance is a missed opportunity.

**What good empty states do:**
1. Acknowledge that nothing is here yet (don't just show a blank box)
2. Explain what will appear here when it's populated
3. Offer a clear call-to-action to create the first item

**Visual options:**
- Illustration (custom or from a library like Undraw)
- Large icon or emoji in a muted color
- Short, friendly headline + one sentence of explanation + CTA button

**Empty state copy examples:**
- ❌ "No items found."
- ✅ "You haven't added any team members yet. Invite your first one to get started."

**Treat every empty state as a feature**, not an afterthought. It's often the first experience a user has with a feature.

---

## Use Fewer Borders

Borders are often the first thing designers reach for when they need to separate content — but they're rarely the best choice. Too many borders make an interface feel cluttered and rigid.

**Alternatives to borders:**

**1. Box shadows**
```css
.card { box-shadow: 0 1px 3px rgba(0,0,0,0.1); }  /* subtle separation without a border */
```

**2. Different background colors**
Adjacent elements with different backgrounds create natural visual separation:
```css
.sidebar { background: var(--grey-50); }
.content { background: white; }
/* No border needed between them */
```

**3. Extra spacing**
Adding more white space between elements communicates "these are separate groups" without drawing a line.

When you do use borders:
- Make them lighter than you think you need (`rgba(0,0,0,0.1)` is often enough)
- Use them for one type of separation in the layout (e.g., only for table rows, not also for cards and sections)

---

## Think Outside the Box

Don't default to the most obvious visual form for a UI component. Most components have been done a thousand times — "breaking the mold" can make your product feel distinctive.

### Examples

**Dropdowns** don't have to be plain white lists. Consider:
- Multiple columns for large option sets
- Icon + label rows
- Section headings within the dropdown
- A description or subtitle under each option

**Tables** don't have to be dense grids. Consider:
- Combining related columns into one cell ("Name + email" in a single cell instead of two columns)
- Using strong hierarchy within a cell (bold primary field, muted secondary field)
- Replacing numerical columns with small charts or progress bars

**Radio buttons** can be replaced with:
- Clickable cards that highlight when selected
- A button group (segmented control)
- An image grid for visual options

**Form labels** can be:
- Floating labels that rise above the field on focus
- Replaced entirely with placeholder text + contextual help icons (for simple forms)

**The key insight:** A component is just an interaction pattern. The visual form it takes is a design decision, not a constraint. Once you understand what a component *does*, you can reinvent how it *looks*.

---

## Leveling Up

To improve at UI design, study work that is better than yours.

**Active strategies:**
1. **Notice design details** in apps you use. When something looks good, ask "why?" — what specific properties (spacing, color, weight, shadow) create the effect?
2. **Rebuild existing UIs** — pick a great screen from Dribbble, Behance, or a product you admire. Try to recreate it pixel-for-pixel. You'll learn what you don't know.
3. **Get into the habit of collecting** UI screenshots that inspire you. Build a reference library.
4. **Follow designers who ship** — designers who build real products have different instincts than those who only create concepts.

The goal is to develop an eye: to be able to look at your own work and immediately see what needs to change, the same way a skilled writer can read a sentence and sense that it's wrong before being able to articulate why.
