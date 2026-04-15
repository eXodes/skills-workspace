# Depth and Imagery Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Creating Depth" and "Working with Images"

---

## Creating Depth

### Emulate a Light Source

Real-world objects are lit from above. UI elements that mimic this feel natural; elements that violate it feel off.

**Consistent light source rule:** If light comes from above, then:
- The top and left edges of raised elements should be **lighter**
- The bottom and right edges should be **darker** (shadowed)
- Inset elements (pressed buttons, text inputs, checkboxes) are the reverse: darker on top/left, lighter on bottom/right

**Raised element** (button, card):
```css
box-shadow: inset 0 1px 0 rgba(255,255,255,0.15),  /* top highlight */
            0 1px 3px rgba(0,0,0,0.15);              /* bottom shadow */
```

**Inset element** (input, checkbox):
```css
box-shadow: inset 0 2px 4px rgba(0,0,0,0.06);  /* top inner shadow */
```

### Don't Get Carried Away

Trying to make every element perfectly mimic real-world lighting leads to cluttered, hard-to-use UI. Borrow a few cues from real-world lighting — you don't need photo-realism.

---

### Use Shadows to Convey Elevation

Shadows communicate how close an element is to the user. Closer = more prominent = larger, softer shadow.

**Shadow scale:**

| Size | CSS example | Use case |
|------|-------------|----------|
| None | — | Flat elements on same z-level |
| Extra small | `0 1px 2px rgba(0,0,0,0.05)` | Subtle lift for cards on white bg |
| Small | `0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06)` | Buttons, input-like elements |
| Medium | `0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06)` | Dropdowns, popovers |
| Large | `0 10px 15px rgba(0,0,0,0.1), 0 4px 6px rgba(0,0,0,0.05)` | Floating cards, sticky elements |
| Extra large | `0 20px 25px rgba(0,0,0,0.1), 0 10px 10px rgba(0,0,0,0.04)` | Modal dialogs, drawer overlays |
| 2xl | `0 25px 50px rgba(0,0,0,0.25)` | Full-screen modals |

**Build an elevation system** the same way you build a color or spacing system. Pick a set of shadows once, name them (sm, md, lg, xl), and only use those values.

---

### Shadows Can Have Two Parts

Real shadows have two layers:
1. **The direct shadow** — caused by direct light being blocked; has a tighter radius, closer to the object
2. **The ambient shadow** — caused by ambient light from the sky; softer and more spread out

Combining both creates a more realistic shadow:

```css
box-shadow:
  0 4px 6px rgba(0, 0, 0, 0.07),   /* ambient */
  0 1px 3px rgba(0, 0, 0, 0.06);   /* direct */
```

This results in shadows that look more "real" than a single shadow layer.

---

### Even Flat Designs Can Have Depth

You don't need shadows to create depth. In flat or "flat-ish" design systems, use color to imply elevation:

- **Lighter surface on a dark background** feels raised
- **Darker surface on a light background** feels inset

```css
/* Flat card on a light grey background */
.card { background: white; }   /* white on #f3f4f6 = slightly raised */

/* Inset section on a white background */
.inset { background: #f9fafb; }  /* light grey on white = recessed */
```

---

### Overlap Elements to Create Layers

Making elements overlap their containers communicates that they exist on different z-levels, without any shadows at all.

**Techniques:**
- Extend an image or avatar slightly above or below its card boundary
- Let a floating action button overlap the header and content area
- Allow a card to break out of a section boundary

This works especially well when shadows would be too subtle to notice, or in flat design systems where you can't use shadows.

---

## Working with Images

### Use Good Photos

Low quality, amateurish photos undermine even the best UI design. Nothing communicates "cheap" faster than a bad stock photo.

**What makes a photo work in UI:**
- Consistent lighting (don't mix studio shots with outdoor photos)
- Professional quality
- Relevant to the content it illustrates
- Not overly staged or "clipart" feeling

**Where to find good photos:**
- Unsplash — high quality, free
- Pexels — large collection, free
- Getty Images / Shutterstock — paid, professional

---

### Text Needs Consistent Contrast

Text over images is a common challenge. Images vary in brightness, so text that's readable in one area is unreadable in another.

**Solutions for text on images:**

**1. Add a semi-transparent overlay**
```css
.hero::after {
  content: '';
  background: rgba(0, 0, 0, 0.45);
  position: absolute; inset: 0;
}
```

**2. Use a gradient**
```css
.hero::after {
  background: linear-gradient(to top, rgba(0,0,0,0.7), transparent);
}
```
Gradient overlays work well when text is only in one area (e.g., a caption at the bottom).

**3. Add text shadows**
```css
.hero-text { text-shadow: 0 1px 3px rgba(0,0,0,0.5); }
```
Works for small text. Not reliable on its own for long body copy.

**4. Colorize the image**
Apply a brand-color overlay with `mix-blend-mode: multiply` to make the image feel on-brand and ensure a predictable background for text.

**5. Overlay a solid color box behind text only**
A translucent pill or rectangle directly behind text is readable and leaves the image visible.

---

### Everything Has an Intended Size

Photos and icons have sizes they're designed for. Misuse them and the result looks wrong.

**Icons:**
- Icons designed for 24px look fuzzy or awkwardly detailed at 64px
- Large icon slots need illustrations or emoji, not scaled-up UI icons
- Don't use a 16px icon at 48px — commission an illustration instead

**Photos:**
- Photos that work as thumbnails don't work as hero images — different framing needed
- Don't stretch portrait photos horizontally (or vice versa) — use `object-fit: cover` to crop instead

**Screenshots:**
- Screenshots of dense interfaces look blurry and unreadable when used small
- Use a specific crop of the most important area, not the full screen

---

### Beware User-Uploaded Content

You can't control the quality, dimensions, or subject matter of user-uploaded photos.

**Protect your layout:**

1. **Always constrain with aspect ratio + `object-fit: cover`**
```css
.avatar { width: 48px; height: 48px; object-fit: cover; border-radius: 50%; }
```

2. **Show a fallback for missing or failed images**
Use initials or a generic placeholder — never a broken image icon.

3. **Don't let images break out of their container**
```css
img { max-width: 100%; height: auto; }
```

4. **For avatars, add a subtle ring/border**
A 1px ring in a light color prevents avatars from bleeding into the background when the photo is very light.
