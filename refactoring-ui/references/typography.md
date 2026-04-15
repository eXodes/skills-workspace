# Typography Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Designing Text"

---

## Establish a Type Scale

Never adjust font sizes one pixel at a time. Define a type scale up front and only use values from it.

### Modular scale approach

A common modular scale (ratio ≈ 1.25):

| Label | px value | Use case |
|-------|----------|----------|
| xs    | 12px     | Labels, captions, helper text |
| sm    | 14px     | Secondary body, small UI text |
| base  | 16px     | Body text |
| lg    | 18px     | Large body, intro paragraphs |
| xl    | 20px     | Small headings, emphasized body |
| 2xl   | 24px     | Section headings |
| 3xl   | 30px     | Page headings |
| 4xl   | 36px     | Large headings |
| 5xl   | 48px     | Hero headings |
| 6xl   | 60px     | Display text |
| 7xl   | 72px+    | Very large display |

**Don't invent intermediate values** like 17px or 22px. The constraint forces intentional decisions and keeps the visual system coherent.

---

## Use Good Fonts

Most UI work calls for a safe, readable font. You don't need an exotic typeface.

### What makes a font good for UI

- Designed for screen readability (not print)
- Has multiple weights (at minimum 400, 600, 700)
- Has a complete character set
- Looks good at small sizes

### Safe choices

**System UI stacks** are always a safe default:
```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
```

**Google Fonts worth knowing:**
- **Inter** — excellent for UI, highly legible, neutral
- **Source Sans Pro** — clean, professional
- **Work Sans** — geometric, modern
- **DM Sans** — friendly, rounded
- **Roboto** — ubiquitous, works well for most UI
- **Playfair Display** — serif, editorial, elegant

### Font selection heuristics

1. **Ignore fonts with less than 5 weights** — you need flexibility for hierarchy
2. **For neutral UI, use a sans-serif** — personality is carried by other elements
3. **For editorial or luxury, consider a serif** — it reads more trustworthy and elegant
4. **For playful UI, use a rounded sans-serif** — the soft corners feel approachable
5. **Steal from great designs** — check what typefaces similar products use

### When to avoid decorative/display fonts for UI

Decorative fonts are for logos and headings, not body text. Script fonts, novelty faces, and overly stylized typefaces are almost always wrong for product UI.

---

## Keep Your Line Length in Check

Long lines are hard to read. The eye struggles to track back to the start of the next line.

**Target:** 45–75 characters per line for body text. Around 20–35em in CSS.

```css
/* Good starting point */
p { max-width: 65ch; }
```

- Below 45 chars: too narrow, text feels choppy
- Above 75 chars: too wide, eye loses its place

For wider layouts, use multiple columns rather than one very wide column.

---

## Baseline, Not Center

When aligning mixed-size text elements (e.g., a large number next to a smaller label), align to the baseline, not the center.

**Center alignment** creates awkward gaps — large text will be hanging above the midpoint, small text below.

**Baseline alignment** makes the reading flow feel natural — the bottom of the letters sit on the same invisible line.

```css
.stat-row { display: flex; align-items: baseline; }
```

This is especially important for:
- Icon + text combinations
- Number + unit combinations ("$45 /month")
- Mixed-size heading + subheading combinations

---

## Line-Height Is Proportional

There's no single correct line-height. The right value depends on line length and font size.

### Rules of thumb

| Situation | Line height |
|-----------|-------------|
| Short lines (narrow column, small text) | 1.3–1.4 |
| Body text (normal column widths) | 1.5–1.6 |
| Wide lines (long-form reading) | 1.7–1.8 |
| Large display/headline text | 1.0–1.2 |

**Wider lines need more line-height.** The eye needs a bigger gap to find the start of the next line.

**Large text needs less line-height.** Headlines look awkward with 1.5 spacing — 1.1–1.2 is typically better.

---

## Not Every Link Needs a Color

By default, browsers style links blue. This is fine on the web, but in dense UI (navigation, sidebars, data tables), not every text element that is a link needs to be blue.

**Use heavier weight instead of color** for links in navigation or tight UI contexts. Reserve the colored underline treatment for body content where users need to identify links in a stream of text.

---

## Align with Readability in Mind

Default to left-aligned text for most content. Centered text and right-aligned text have specific use cases.

| Alignment | Best for |
|-----------|----------|
| Left | Body text, any content longer than a few words |
| Center | Short hero text, card titles, small UI captions |
| Right | Numbers in data tables (makes columns scannable), form labels next to inputs |
| Justify | Avoid — creates inconsistent spacing between words |

**Don't center-align long paragraphs.** It creates an uneven left edge that makes reading exhausting.

---

## Use Letter-Spacing Effectively

Most fonts are designed for sentence-case body text. The default letter-spacing is optimized for that context.

### All-caps text

All-caps text lacks variety (no ascenders/descenders, uniform height). This makes letters harder to distinguish, so **increase letter-spacing for all-caps text**.

```css
.label { text-transform: uppercase; letter-spacing: 0.05em; }
```

### When NOT to add letter-spacing

- Normal body text — the font's default is already optimized
- Large display text — adding letter-spacing to already-large headlines often looks loose and amateurish

### Tight letter-spacing

Some modern designs use slightly negative letter-spacing on large headings (`-0.01em` to `-0.02em`) for a sleek, condensed look. Use sparingly.
