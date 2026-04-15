# Typography Readability Fix

**Category:** Typography — Line length, Line-height

You have two compounding problems here. Both are fixable with small, precise changes.

---

## Line-Height Proportional to Line Length — **significant**

**Where:** Body text (`p` or equivalent container)

**Why it matters:** Your 1.2 line-height is the correct value for *large display and headline text*, not body text — it squashes lines together and forces the reader's eye to work hard to separate one line from the next.

**Fix:**
- For a normal column width (45–75 chars), use `line-height: 1.5` or `line-height: 1.6`.
- Because your container is currently full-width (long lines), you should actually go even higher: **`line-height: 1.7`** until you fix the container width (see below).
- Once you constrain the line length with a `max-width`, you can dial back to `1.5–1.6`.

```css
p {
  line-height: 1.6; /* after adding max-width below */
}
```

---

## Line Length Control (Max-Width) — **significant**

**Where:** Body text container (full-width layout)

**Why it matters:** A full-width container on any reasonably wide screen will produce lines well beyond 75 characters. The eye loses its place finding the start of the next line, which is exactly the fatigue you're describing.

**Fix:**
- Add a `max-width` to your paragraph or content container. The canonical target is **45–75 characters per line**.
- In CSS, `ch` units are your best tool: **`max-width: 65ch`** is an excellent default for body text.
- If you need a pixel fallback on a 16px font, ~640–700px is approximately equivalent.

```css
p {
  max-width: 65ch;
  line-height: 1.6;
}
```

For a wider editorial layout, you can go up to `75ch`, but never leave it unconstrained. If you have a multi-column layout, distribute text across columns rather than stretching one column full-width.

---

## Summary of Changes

| Property | Before | After |
|---|---|---|
| `font-size` | 16px | 16px ✅ (already correct for body) |
| `line-height` | 1.2 | 1.6 |
| container `max-width` | full-width | `65ch` |

Your font size of 16px is fine — that's the standard `base` body size and needs no change. The two problems are entirely the line-height and the missing width constraint.

---

## Related Issue Worth Noting

**Line-height is proportional, not fixed.** If you have any headings or large display text in the same layout, make sure *those* stay at 1.0–1.2 — the same value you're currently using for body text. The inverse mistake (applying body line-height to headlines) makes headings look airy and disconnected. Keep the 1.2 for `h1`/`h2`, and use 1.5–1.6 exclusively for reading-length body copy.
