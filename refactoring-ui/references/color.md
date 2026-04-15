# Color Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Working with Color"

---

## Ditch Hex for HSL

Hex (`#2563EB`) and RGB (`rgb(37, 99, 235)`) represent colors as machine values with no human-readable structure. Similar-looking colors look nothing alike in hex.

**HSL** (Hue, Saturation, Lightness) maps to how humans perceive color:

| Component | Meaning | Range |
|-----------|---------|-------|
| **Hue** | Position on the color wheel (red, green, blue, etc.) | 0°–360° |
| **Saturation** | How vivid/colorful (0% = grey, 100% = vibrant) | 0%–100% |
| **Lightness** | How light or dark (0% = black, 100% = white) | 0%–100% |

**Why this matters:** In HSL, building a color scale is intuitive — keep the hue fixed, vary lightness and saturation. In hex, this requires guesswork.

```css
/* Primary blue in HSL */
--blue-50:  hsl(217, 91%, 95%);  /* very light tint */
--blue-500: hsl(217, 91%, 60%);  /* main brand color */
--blue-900: hsl(217, 91%, 20%);  /* very dark shade */
```

---

## You Need More Colors Than You Think

A real UI needs colors for many purposes. Plan for at least three categories.

### The three categories

**1. Greys** — text, backgrounds, borders, dividers
You need 8–10 shades from near-white to near-black. Greys are used everywhere, so having a full range is essential.

**2. Primary color(s)** — your brand color; used for primary actions, active states, links, focus rings
You need 5–10 shades, from very light (hover backgrounds, tints) to very dark (pressed states, text on light backgrounds).

**3. Accent colors** — semantic colors and supporting palette
- **Danger/Error** — red, used sparingly for errors and destructive actions
- **Warning** — yellow/amber, used for alerts
- **Success** — green, used for confirmations and positive states
- **Info** — blue or teal, used for informational messages
- Each needs its own light, medium, and dark shades (at least 3, ideally 5–7)

---

## Define Your Shades Up Front

Don't reach for the color picker every time you need a shade of blue. Define your whole palette once, then only use those values.

### A 9-shade scale per color

| Step | Typical lightness | Use case |
|------|-------------------|----------|
| 50   | ~95%              | Very light backgrounds, hover states |
| 100  | ~90%              | Light backgrounds, tinted sections |
| 200  | ~80%              | Borders on light backgrounds |
| 300  | ~70%              | Disabled states, subtle fills |
| 400  | ~60%              | Placeholder text, subtle icons |
| 500  | ~50%              | Brand/primary color (main) |
| 600  | ~40%              | Hover state on primary button |
| 700  | ~30%              | Active/pressed states |
| 800  | ~20%              | Dark text, dark mode backgrounds |
| 900  | ~10%              | Very dark text, high-contrast |

**Choosing the base first:** Start with the color that looks "right" as your main brand color — usually in the 400–600 range. Then build lighter and darker shades around it.

### The perceptual lightness problem

HSL's lightness is not perceptual. A yellow at 50% HSL lightness appears much lighter than a blue at 50%. When building your palette, you may need to tweak saturation as you adjust lightness to make shades feel evenly distributed.

**Tip:** As you go lighter (higher lightness), you often need to *increase* saturation to avoid the color looking washed out. As you go darker, saturation often needs to decrease.

---

## Don't Let Lightness Kill Your Saturation

Light shades of a color tend to look grey and muddy if you only change the lightness and not the saturation.

**Fix:** When creating light tints, nudge the saturation up. When creating dark shades, nudge it down slightly. The goal is for each shade in your scale to feel like a genuine version of the color — not a diluted or dead version.

**Also:** Rotating the hue slightly as you move through the scale can help:
- For light shades: rotate toward a hue that appears lighter perceptually (yellows/greens)
- For dark shades: rotate toward a hue that appears darker perceptually (blues/purples)

This is what makes hand-crafted palettes look better than purely algorithmic ones.

---

## Greys Don't Have to Be Grey

Pure grey (hue 0°, saturation 0%) often looks clinical and cold. Greys with a slight hue feel more natural and professional.

**Warm greys** (slight yellow/red hue) → feel cozy, traditional, editorial
**Cool greys** (slight blue hue) → feel modern, technical, clean

Use warm greys when your brand color is warm (orange, red, yellow). Use cool greys when your brand is cool (blue, purple, teal). This creates cohesion between greys and the rest of your palette.

```css
/* Cool grey */
--grey-500: hsl(220, 9%, 46%);

/* Warm grey */
--grey-500: hsl(30, 6%, 46%);
```

---

## Accessible Doesn't Have to Mean Ugly

WCAG contrast requirements exist for good reason. Don't ignore them — but don't assume meeting them requires ugly, over-saturated colors.

### Contrast ratios (WCAG 2.1)

| Level | Normal text | Large text (≥18px or ≥14px bold) |
|-------|-------------|----------------------------------|
| AA    | 4.5:1       | 3:1                              |
| AAA   | 7:1         | 4.5:1                            |

**Check your contrast.** Tools: [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/), browser devtools accessibility panels.

### Common accessibility mistakes

- White text on a light-colored background (even if the color "looks dark enough", check it)
- Light grey text on white (common, and often fails AA)
- Relying on a single branded color (e.g., medium blue) for both buttons and body text — the same color may fail for one of these uses

### Fixing contrast without sacrificing aesthetics

- Use a darker shade from your palette for text/icons instead of the main brand color
- Darken the background instead of changing the text color
- Use a different shade specifically for accessibility-critical elements

---

## Don't Rely on Color Alone

Color is not reliable for conveying meaning by itself — some users are colorblind (~8% of males have red-green color blindness), and others use screen readers.

**Always pair color with a secondary signal:**

| Use case | Color + what else |
|----------|-------------------|
| Error state | Red + error icon + error text |
| Success state | Green + checkmark icon |
| Warning | Yellow/amber + warning icon |
| Disabled | Muted color + reduced opacity + cursor: not-allowed |
| Active/selected | Brand color + bold weight or border/underline |

**Graphs and charts:** Don't differentiate data series by color alone. Add labels, patterns, or shape markers.

**Forms:** Don't indicate a required field only with a red asterisk. Use label text too.
