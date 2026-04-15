# Fixing Form Label-to-Input Spacing

## The Core Problem: Proximity

When labels and inputs feel jumbled, it's almost always a **proximity problem**. The visual distance between a label and its input should be *smaller* than the distance between consecutive form groups. If all gaps are equal, the eye can't group them.

## The Fix: Unequal Spacing

Use the **law of proximity** deliberately:

```
[Label A]        ← close to its input (e.g., 4–6px gap)
[Input A]

                 ← larger gap between groups (e.g., 24–32px)

[Label B]        ← close to its input (e.g., 4–6px gap)
[Input B]
```

The space *between* groups should be **3–5× larger** than the space between a label and its own input.

### Recommended values (as a starting point):
- Label → Input gap: `4px–8px`
- Input → Next label gap: `20px–32px`

---

## Specific Techniques

### 1. Reduce label-to-input spacing
Set `margin-bottom` on labels to a small value (e.g., `4px`). This visually "attaches" the label to its field.

```css
label {
  display: block;
  margin-bottom: 4px;
}
```

### 2. Increase spacing between form groups
Wrap each label+input pair in a container and space those containers apart.

```css
.form-group {
  margin-bottom: 24px;
}
```

### 3. Use consistent alignment
- **Left-aligned labels above inputs** are the easiest to scan and pair visually — especially in single-column forms.
- Avoid inline labels at the same size/weight as surrounding text; they blend in.

### 4. Differentiate label typography
Make labels visually distinct from input text so the hierarchy is clear:
- Slightly smaller font size (e.g., `12px–13px` vs `16px` for input text)
- Heavier weight (`500` or `600`)
- Muted color (e.g., `#6B7280` instead of full black)

---

## Quick Diagnostic Checklist

| Problem | Fix |
|---|---|
| Label floats far above input | Reduce `margin-bottom` on label |
| Groups bleed into each other | Increase `margin-bottom` on `.form-group` |
| Can't tell label from regular text | Adjust weight, size, or color of labels |
| Inline labels feel cramped | Switch to stacked (label above input) layout |

---

## Summary

The single most impactful change: **make the gap between a label and its input smaller than the gap between two separate form groups.** Everything else (typography, color) is secondary to getting the spatial relationships right.
