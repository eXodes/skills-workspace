# Empty State Design

## Don't Overlook Empty States — significant
**Where:** Any section, list, or content area that has no data yet  
**Why it matters:** A blank white area is a missed opportunity — empty states are often the *first* experience a new user has with a feature, and a blank box communicates nothing about what the product does or how to get started.

---

### What's Wrong with a Blank White Area

A blank white area fails on three levels:

1. **It doesn't acknowledge the absence of content.** Users don't know if something is broken, loading, or just empty.
2. **It doesn't explain what will appear here.** Without context, users can't understand the feature's purpose.
3. **It doesn't guide the user toward an action.** There's no nudge to create the first item — so many users simply leave.

---

### The Three Jobs of a Good Empty State

Every empty state should do these three things:

1. **Acknowledge** that nothing is here yet (don't just show a blank box)
2. **Explain** what will appear here when the section is populated
3. **Offer a clear call-to-action** to create the first item

---

### How to Apply This

**Copy first — get the words right before the visuals:**

- ❌ "No items found."
- ✅ "You haven't added anything yet. Create your first one to get started."

Friendly, specific copy transforms a dead end into an invitation.

**Then add a visual element. Pick one:**

- **Illustration** — a custom or library illustration (e.g., from Undraw) that relates to the content type. Best for prominent empty states in core product areas.
- **Large icon in a muted color** — a simple icon representing the content type, displayed large, in a light grey or your brand color at low opacity. Lower effort, still effective.
- **Emoji** — works for casual or consumer-facing apps; feels approachable and quick to implement.

**Then add a CTA button:**

Place a primary action button directly in the empty state — "Add Team Member", "Create Project", "Upload Your First File". The button should be the same primary button you use elsewhere in the UI; don't invent a new style for it.

**A typical empty state layout:**
```
[Illustration or Icon]
  "You haven't added any [items] yet."
  "Create your first [item] to get started."
  [  + Add [Item]  ]   ← primary button
```

Center this block vertically and horizontally within the empty area. Give it generous padding so it doesn't feel cramped against the container edges.

---

### Treat Every Empty State as a Feature

Empty states aren't an afterthought — they're a product design moment. A well-crafted empty state:

- Reassures users that the product is working correctly
- Sets expectations for what the feature will do
- Reduces friction by providing a direct path to the first action
- Can even communicate your brand personality through tone and illustration style

---

## Related Issues to Check

### Background decoration — minor
**Where:** The container holding the empty state  
**Why it matters:** A pure white box can feel blank even when the empty state copy is in place.  
**Fix:** Give the empty state section a subtly tinted background — `hsl(220, 30%, 98%)` instead of pure white — or a very faint dot-grid pattern at low opacity. This makes the area feel intentional rather than "nothing loaded."

### Fewer borders — minor
**Where:** The border you may be using to define the empty area  
**Why it matters:** A box drawn with a border around empty space can feel sad and clinical.  
**Fix:** Instead of a hard border to define the section, try a box shadow (`box-shadow: 0 1px 3px rgba(0,0,0,0.08)`) or just extra padding and a background color difference. If you're already using a border, consider making it dashed — a dashed border is a common convention that communicates "placeholder / not yet filled" more intentionally than a solid line.
