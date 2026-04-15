# Shadow Values for Modal Dialogs vs. Tooltips

## Elevation System Collapse — Significant
**Where:** Both the modal dialog and the tooltip  
**Why it matters:** Using the same box shadow for both elements communicates that they sit at the same perceived height above the page — but they don't. A modal is one of the highest-elevation elements in any UI; a tooltip is smaller and more ephemeral. Giving them identical shadows flattens your elevation system and removes a key visual cue that tells users *how far from the page* each element is.

---

## The Core Principle: Shadows Communicate Elevation

From Refactoring UI: **closer = more prominent = larger, softer shadow.**

Shadows don't just add decoration — they convey how high an element floats above the page surface. A larger, more spread-out shadow implies the element is further from the page (casting a wider shadow). A tighter, smaller shadow implies it's close to the surface.

This is the same reason real objects cast different shadows depending on how high they are — hold a book 1cm above a table vs. 30cm above it and the shadows look completely different.

---

## Recommended Shadow Values

### Modal Dialog → Extra Large Shadow

Modals sit at the *top* of the z-layer stack. They block the entire background, demand user attention, and represent the highest-elevation element in most UIs. Use the extra large shadow:

```css
/* Modal dialog */
box-shadow:
  0 20px 25px rgba(0, 0, 0, 0.1),   /* ambient — wide, soft */
  0 10px 10px rgba(0, 0, 0, 0.04);  /* direct — tighter, closer to object */
```

For a full-screen or very large modal, go up to 2xl:

```css
/* Full-screen modal */
box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
```

**Why:** The large vertical offsets (`20px–25px`) and wide spread communicate that this element is far above the page surface. The two-layer approach (ambient + direct shadow) adds realism — real shadows have both a tight direct component and a soft ambient component.

---

### Tooltip → Medium Shadow

Tooltips are closer in character to dropdowns and popovers — small, contextual, lightweight. They should use a medium shadow:

```css
/* Tooltip */
box-shadow:
  0 4px 6px rgba(0, 0, 0, 0.07),   /* ambient */
  0 2px 4px rgba(0, 0, 0, 0.06);   /* direct */
```

**Why:** The smaller offsets (`4px–6px`) signal that the tooltip floats above the page but not by much. A heavy shadow on something small looks incongruous — the shadow would be larger than the element deserves. The two-part structure still applies, just at a smaller scale.

---

## Why They Must Be Different

| Element | Shadow scale | Reason |
|---------|-------------|--------|
| Tooltip | Medium | Small, ephemeral, informational — sits just above the surface |
| Modal dialog | Extra Large / 2xl | Demands full attention, blocks the page, highest elevation in the stack |

If both use the same shadow, your UI loses a layer of communication. When a tooltip appears over a modal (which it sometimes can), the user gets no visual signal about which element is "closer." More broadly, a flat elevation system makes the UI feel less spatially coherent — elements seem to arbitrarily float rather than occupy logical layers.

---

## Build a Named Elevation System

Rather than hardcoding these two values and moving on, treat shadows the same way you'd treat a color palette or spacing scale — define a small set of named levels and only use those:

```css
--shadow-sm:  0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06);     /* buttons */
--shadow-md:  0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06);    /* tooltips, dropdowns */
--shadow-lg:  0 10px 15px rgba(0,0,0,0.1), 0 4px 6px rgba(0,0,0,0.05);   /* floating cards */
--shadow-xl:  0 20px 25px rgba(0,0,0,0.1), 0 10px 10px rgba(0,0,0,0.04); /* modals, drawers */
--shadow-2xl: 0 25px 50px rgba(0,0,0,0.25);                               /* full-screen overlays */
```

Decide once, name them, and apply consistently. This makes elevation feel intentional rather than ad hoc.

---

## One Related Issue Worth Noting

**Light source consistency:** If your modal or tooltip uses a directional shadow, make sure the shadow direction matches the rest of your UI. A shadow pointing down-right on a card but straight down on your modal signals that "light" comes from two different places — which feels subtly wrong. Pick a consistent vertical offset direction (most commonly straight down or slightly down-right) and apply it everywhere.
