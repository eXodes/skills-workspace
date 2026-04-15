# Typography Fix: Body Text Readability

## The Problems

Your setup — 16px font, 1.2 line-height, full-width container — has three compounding issues:

### 1. Line Height is Too Tight
`1.2` line-height is appropriate for headings, not body text. For running prose, the eye needs more vertical breathing room to track from the end of one line back to the start of the next.

**Fix:** Use `1.5` to `1.7` line-height for body text. A value of `1.6` is a solid default.

```css
body {
  line-height: 1.6;
}
```

### 2. Line Length is Too Long
A full-width container can easily produce 100–150+ characters per line depending on screen size. The readable ideal is **45–75 characters per line** (roughly 60ch). Long lines force the eye to travel too far horizontally, making it hard to find the next line.

**Fix:** Constrain your text container with `max-width`:

```css
.content {
  max-width: 65ch; /* or roughly 680px */
  margin-inline: auto;
}
```

Using `ch` units is ideal because it scales with the font size.

### 3. Font Size Could Be Larger (Optional but Recommended)
16px is the minimum acceptable baseline for body text. On larger screens, bumping to `18px` or `20px` significantly improves comfort, especially for longer reading sessions.

```css
body {
  font-size: 18px;
}
```

---

## Summary of Fixes

| Property | Current | Recommended |
|---|---|---|
| `font-size` | 16px | 18–20px |
| `line-height` | 1.2 | 1.5–1.7 |
| Container width | Full-width | `max-width: 60–75ch` |

## Why These Rules Exist

- **Line height** affects vertical rhythm. Too tight and descenders visually collide with ascenders on the next line, making text feel dense.
- **Line length** (measure) affects how easily the eye returns to the start of the next line. Too wide and readers lose their place; too narrow and the eye jumps too frequently.
- **Font size** interacts with both — a larger font naturally shortens the effective line length in character count for any given pixel width.

Applying all three fixes together will make your body text dramatically more comfortable to read.
