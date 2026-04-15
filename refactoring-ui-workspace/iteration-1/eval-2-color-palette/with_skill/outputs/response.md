# Building a Full Color Palette for a Fintech App (Blue as Primary)

**Category:** Color — palette structure, HSL, 9-shade scale, greys, semantic colors, accessibility

---

## Step 1: Ditch Hex — Work in HSL

Before touching a color picker, switch your mental model to **HSL** (Hue, Saturation, Lightness). Hex and RGB are machine values with no human-readable structure — similar-looking blues look nothing alike in hex. HSL maps to how you perceive color:

| Component | What it controls | Range |
|-----------|-----------------|-------|
| Hue | Which color on the wheel | 0°–360° |
| Saturation | How vivid vs. grey | 0%–100% |
| Lightness | How light vs. dark | 0%–100% |

In HSL, building a full blue scale is systematic: keep the hue fixed, vary lightness and saturation. In hex, it's guesswork.

For a fintech app with a professional, trustworthy feel, a good base hue is around **217°** — a clean, medium blue that reads as financial/institutional without being cold.

---

## Step 2: Understand the Three Color Categories You Need

A real UI needs more colors than just "blue." Plan for three categories from the start:

### 1. Greys (8–10 shades)
Used everywhere — text, backgrounds, borders, dividers, disabled states. This is your most-used palette. Don't skip it.

### 2. Primary Color (9 shades)
Your blue. Used for primary actions (CTA buttons), active nav, links, focus rings, progress indicators, and key data highlights.

### 3. Semantic / Accent Colors (5–7 shades each)
- **Danger / Error** — red (form errors, destructive actions, overdraft warnings)
- **Warning** — amber/yellow (alerts, approaching limits)
- **Success** — green (transaction confirmed, balance positive)
- *(Optional)* **Info** — teal or lighter blue (informational banners)

Each semantic color needs enough shades to cover: background tint, border, icon/text color on both light and dark surfaces.

---

## Step 3: Build Your 9-Shade Primary Blue Scale

**Start by choosing your 500 — the base brand color.** This is what appears on buttons, active links, and key UI chrome. It should look right at face value: vivid, clearly blue, not too light and not so dark it loses energy. For fintech, `hsl(217, 91%, 55%)` is a solid starting point — adjust to taste.

Then build outward from 500 in both directions.

```css
/* Primary Blue — hue 217° */
--blue-50:  hsl(217, 100%, 97%);   /* page-level tinted backgrounds, hover fill */
--blue-100: hsl(217,  96%, 92%);   /* section backgrounds, tag fills */
--blue-200: hsl(217,  93%, 83%);   /* borders on light backgrounds */
--blue-300: hsl(217,  89%, 72%);   /* disabled states, subtle fills */
--blue-400: hsl(217,  87%, 63%);   /* placeholder text, subtle icons */
--blue-500: hsl(217,  91%, 55%);   /* ← main brand color: buttons, links */
--blue-600: hsl(217,  83%, 45%);   /* button hover state */
--blue-700: hsl(217,  76%, 35%);   /* button active/pressed state */
--blue-800: hsl(217,  68%, 25%);   /* dark text on light blue backgrounds */
--blue-900: hsl(217,  60%, 15%);   /* high-contrast text, dark mode surfaces */
```

### The Perceptual Lightness Problem — Don't Ignore It

HSL lightness is **not perceptual**. A blue at 50% lightness looks darker than a yellow at 50% lightness. If you just slide the lightness value and do nothing else, your light shades will look washed out and muddy.

**Fix:**
- As you go **lighter** (50 → 100 → 200): **increase saturation** to compensate. A blue-50 at low saturation looks like a grey fog — push saturation up toward 96–100% to keep it reading as genuinely blue.
- As you go **darker** (500 → 700 → 900): **decrease saturation slightly**. Very dark blues with full saturation can look unnatural. Nudge it down as you go deeper.

This is what separates a hand-crafted palette from a purely algorithmic one — and it's the main reason palettes feel flat or alive.

**Optional advanced technique:** Rotate hue slightly as you move through the scale:
- Light shades → nudge hue toward 210–215° (slightly toward cyan/green, which appears perceptually lighter)
- Dark shades → nudge hue toward 220–225° (slightly toward indigo/purple, which appears perceptually darker)

This is subtle but makes each shade feel like a genuine version of the color rather than a diluted or dead version.

---

## Step 4: Build Cool Greys (Not Pure Grey)

Since your brand is blue — a cool color — use **cool greys** (slight blue hue). Pure greys at hue 0°, saturation 0% look clinical and generic. A slight hue makes them feel like part of a coherent system.

```css
/* Cool Greys — hue 220° */
--grey-50:  hsl(220, 20%, 98%);   /* page background */
--grey-100: hsl(220, 16%, 94%);   /* card backgrounds, sidebar */
--grey-200: hsl(220, 14%, 88%);   /* borders, dividers */
--grey-300: hsl(220, 12%, 78%);   /* light borders, disabled borders */
--grey-400: hsl(220, 10%, 65%);   /* placeholder text, disabled icons */
--grey-500: hsl(220,  9%, 52%);   /* secondary body text */
--grey-600: hsl(220, 10%, 40%);   /* secondary text (stronger) */
--grey-700: hsl(220, 12%, 30%);   /* primary body text */
--grey-800: hsl(220, 14%, 20%);   /* headings */
--grey-900: hsl(220, 16%, 12%);   /* near-black, high-contrast labels */
```

> **Rule:** Warm brand = warm greys. Cool brand = cool greys. Your blue fintech app should use cool greys throughout.

---

## Step 5: Build Semantic Color Scales

Each semantic color also needs a 5–7 shade scale. You don't necessarily need all 9 — but you need at minimum: a light background tint (for alert banners), a mid tone (for icons/borders), and a dark tone (for text on light backgrounds).

Here's a complete set for a fintech app:

### Danger / Error — Red (hue ~4°)
```css
--red-50:  hsl(4, 100%, 97%);   /* error banner background */
--red-100: hsl(4,  96%, 91%);   /* error input fill */
--red-200: hsl(4,  90%, 82%);   /* error input border */
--red-400: hsl(4,  87%, 65%);   /* error icon */
--red-500: hsl(4,  91%, 55%);   /* primary error color */
--red-700: hsl(4,  76%, 35%);   /* error text on light background */
--red-900: hsl(4,  60%, 16%);   /* dark error text */
```

### Warning — Amber (hue ~38°)
```css
--amber-50:  hsl(38, 100%, 96%);  /* warning banner background */
--amber-100: hsl(38,  96%, 89%);
--amber-200: hsl(38,  90%, 79%);
--amber-400: hsl(38,  90%, 60%);  /* warning icon */
--amber-500: hsl(38,  92%, 50%);  /* primary warning color */
--amber-700: hsl(38,  78%, 35%);  /* warning text on light bg */
--amber-900: hsl(38,  62%, 18%);
```

### Success — Green (hue ~145°)
```css
--green-50:  hsl(145, 80%, 96%);  /* success banner background */
--green-100: hsl(145, 76%, 88%);
--green-200: hsl(145, 70%, 76%);
--green-400: hsl(145, 68%, 52%);  /* success icon */
--green-500: hsl(145, 72%, 44%);  /* primary success color */
--green-700: hsl(145, 62%, 30%);  /* success text on light bg */
--green-900: hsl(145, 50%, 16%);
```

> **Fintech-specific note:** In financial UIs, red and green carry strong semantic meaning (loss/gain, debit/credit). Ensure your danger red and success green are visually distinct and always paired with icons and text — never color alone.

---

## Step 6: Accessibility — Check Your Contrast

WCAG 2.1 minimums for your fintech app:

| Level | Normal text (< 18px) | Large text (≥ 18px or ≥ 14px bold) |
|-------|---------------------|-------------------------------------|
| AA    | 4.5:1               | 3:1                                 |
| AAA   | 7:1                 | 4.5:1                               |

**Common traps with blue palettes:**
- White text on `--blue-400` or `--blue-500` — often **fails AA**. Use `--blue-600` or `--blue-700` for buttons with white text.
- `--grey-400` text on white — often fails. Use `--grey-600` or darker for body text.
- Blue on blue (e.g., a blue link inside a blue banner) — nearly always fails. Use `--blue-900` text on `--blue-50` backgrounds.

**Quick rule:** For white text on a colored button, use shade 600 or 700, not 500. For colored text on a white background, use shade 700 or 800.

Check every combination at [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).

---

## Step 7: Never Use Color Alone

About 8% of males have red-green color blindness. In a fintech app where color communicates gain/loss, success/failure, and alerts, this is critical.

**Always pair color with a secondary signal:**

| Use case | Color + what else |
|----------|-------------------|
| Transaction failed | Red + ✕ error icon + "Payment failed" text |
| Transfer confirmed | Green + ✓ checkmark + "Sent successfully" |
| Balance warning | Amber + ⚠ icon + "Low balance" label |
| Active nav item | Blue + bold weight or left border indicator |
| Disabled button | Muted grey + `cursor: not-allowed` |
| Required field | Red asterisk + "Required" label text |

Charts showing portfolio performance must never rely on color alone to differentiate series — add labels, patterns, or shape markers.

---

## Summary: Your Fintech Palette at a Glance

| Token group | Shades | Primary use |
|-------------|--------|-------------|
| `--blue-*`  | 50–900 | CTAs, links, active states, focus rings, key data |
| `--grey-*`  | 50–900 | Text, backgrounds, borders, dividers |
| `--red-*`   | 50–900 | Errors, destructive actions, loss indicators |
| `--amber-*` | 50–900 | Warnings, approaching limits, caution states |
| `--green-*` | 50–900 | Success, confirmation, gain indicators |

**Build order:**
1. Pick `--blue-500` (your brand color at face value)
2. Build 8 more blue shades, adjusting saturation at each step
3. Build cool greys (same hue as blue, low saturation)
4. Add red, amber, green with 5–7 shades each
5. Check all foreground/background combinations for contrast
6. Audit every color usage to ensure a secondary signal exists alongside color
