# Modal vs. Tooltip Box Shadows — Why They Should Be Different

## The Core Principle: Shadows Communicate Elevation

In UI design, box shadows don't just add visual polish — they simulate depth. The size and diffusion of a shadow tells users how far an element is "lifted" off the surface. Using the same shadow for a modal and a tooltip breaks this spatial metaphor, making your UI feel incoherent.

---

## Recommended Shadow Values

### Modal Dialog
```css
box-shadow:
  0 20px 60px rgba(0, 0, 0, 0.30),
  0 8px 20px rgba(0, 0, 0, 0.15);
```
- **Large vertical offset** (20px): Simulates a light source casting a long shadow from a high elevation
- **Large blur radius** (60px): Soft, diffuse shadow — objects far from a surface spread their shadow widely
- **Higher opacity**: The shadow needs to be readable over a dimmed backdrop and regular page content
- **Layered shadow**: A second, tighter shadow adds depth realism

### Tooltip
```css
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
```
- **Small vertical offset** (4px): Tooltips sit just slightly above the page
- **Tight blur radius** (12px): A focused shadow for a compact element at low elevation
- **Low opacity**: Tooltips are ephemeral — an aggressive shadow would make them feel too heavy

---

## Why They Must Be Different

### 1. Elevation Hierarchy
Modals represent **high elevation** — they float far above the page and block interaction with everything underneath. Tooltips are **low elevation** — a small label that barely lifts off the surface. Matching shadow values collapses this distinction and makes the UI spatially confusing.

### 2. Visual Weight Matches Purpose
A modal demands your attention. It may require you to make a decision before proceeding. Its shadow should reinforce this gravity. A tooltip is transient supplementary information — a heavy shadow would make it feel as important as the modal, which misrepresents the hierarchy.

### 3. Proportionality
Shadow should scale with the element's size. A large, full-screen-width modal paired with a small tooltip shadow would look like it's barely floating. The same large shadow applied to a small tooltip makes the shadow bigger than the element itself — visually absurd.

### 4. Backdrop Context
Modals typically render over a semi-transparent scrim/overlay. Without a strong shadow, the modal can visually blend into or feel disconnected from the darkened backdrop. Tooltips have no backdrop — they appear over live UI — and a subtle shadow is enough to establish separation without overwhelming nearby content.

### 5. The "Real World" Analogy
Think of a sheet of paper resting on a table (tooltip) vs. a sheet of glass lifted several inches above it (modal). Objects close to a surface cast short, tight, dark shadows. Objects far from a surface cast long, wide, diffuse shadows. Your CSS should mirror this physics.

---

## Summary Table

| Property | Modal | Tooltip | Reason |
|---|---|---|---|
| Y-offset | Large (20px+) | Small (2–4px) | Elevation height |
| Blur radius | Large (40–80px) | Small (8–16px) | Distance from surface |
| Opacity | Medium-high (25–35%) | Low (10–20%) | Visual weight & context |
| Layers | Often 2 shadows | Single shadow | Realism vs. simplicity |

---

## The Takeaway

Use the same shadow system — not the same shadow value. Define a shadow scale (like `shadow-sm`, `shadow-md`, `shadow-xl`) and assign modals to the highest tier and tooltips to a lower tier. This creates visual consistency while maintaining correct spatial hierarchy throughout your UI.
