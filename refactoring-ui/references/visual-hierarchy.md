# Visual Hierarchy Reference

Source: Refactoring UI by Adam Wathan & Steve Schoger — "Hierarchy is Everything"

---

## Core Principle

Visual hierarchy is how important elements appear relative to one another. When everything competes for attention, the result is noise. When you deliberately de-emphasize secondary and tertiary content and highlight what matters most, the result looks "designed" — even without changing colors, fonts, or layout.

---

## Size Isn't Everything

Relying only on font size to create hierarchy leads to primary content that's too large and secondary content that's too small.

**Three tools for hierarchy** (use them together):
1. **Font size** — primary differentiator, but don't overuse it
2. **Font weight** — bold draws attention without changing size
   - Normal weight (400–500) for most text
   - Heavy weight (600–700) for emphasis
   - Avoid weights below 400 for UI — too hard to read at small sizes
3. **Color** — use a limited palette of 2–3 levels:
   - Dark color for primary content (headlines, key data)
   - Grey for secondary content (subtitles, dates, metadata)
   - Lighter grey for tertiary content (footnotes, copyright)

**Instead of making secondary text tiny, make it lighter (lower contrast).** The readability cost of small text is higher than the readability cost of muted color.

---

## Don't Use Grey Text on Colored Backgrounds

Grey text works on white because it reduces contrast. On a colored background, grey doesn't reduce contrast — it just looks muddy.

**On colored backgrounds, de-emphasize by using a color closer to the background** (lower opacity white, or a tint of the background color), not by using grey.

- On a blue background: use `rgba(255,255,255,0.7)` instead of `#999`
- On a dark background: use `rgba(255,255,255,0.6)` for secondary text

---

## Emphasize by De-emphasizing

Sometimes the best way to make something stand out is to make everything else less prominent.

**Example:** If you can't make a primary element stand out by styling it more aggressively, try toning down everything else instead. Remove bold from secondary items, lighten supporting text, reduce the weight of nearby decorative elements.

This works because hierarchy is relative — primary content only needs to be more prominent than the secondary content around it.

---

## Labels Are a Last Resort

Every piece of data doesn't need a label. Labels interrupt the reading flow and add visual noise.

### When you don't need labels:
- **The format implies the content:** An email address, phone number, URL, or date is self-explanatory
- **Context makes it obvious:** Inside a "Messages" section, a person's name and avatar don't need a "Sender:" label
- **The data is the content:** A large "$149/mo" price doesn't need "Price:" before it

### When you do need labels:
- When the data is ambiguous without context (e.g., "1234567" — is that a phone number, an ID, a zip code?)
- In dense data tables where many similar values appear together

### When labels are unavoidable:
Make them secondary. De-emphasize the label (light weight, muted color) and let the value be the primary element.

**Avoid the "label: value" pattern everywhere.** It's lazy. Think about whether the value can stand alone.

---

## Separate Visual Hierarchy from Document Hierarchy

HTML heading levels (h1, h2, h3) are about document structure, not visual importance. Don't conflate them.

An `h2` section title might actually need to be visually smaller and lighter than the primary content beneath it, if the content is what the user cares about.

**Example:** A "Published by" label above a large author name. Semantically the label is higher in document hierarchy, but visually the author name should dominate.

Style for the user's reading flow, not for semantic correctness. Use appropriate HTML structure for accessibility, but override visual presentation with CSS.

---

## Balance Weight and Contrast

Icons and other non-text elements often have more visual weight than text at the same size. An icon next to a heading can feel "heavier" and pull attention away.

**Technique for balancing:**
- Reduce icon opacity (e.g., 40–60%) to lower its contrast against the background
- This makes it feel secondary without removing it

The same applies to borders, dividers, and decorative elements — they often need to be more subtle than your first instinct.

---

## Semantics Are Secondary

Don't let semantic meaning dictate visual prominence.

### Primary, Secondary, and Tertiary Actions

On a page with multiple actions, not all buttons should look the same. Use visual weight to communicate importance:

- **Primary action** → solid, high-contrast button
- **Secondary actions** → outline style or lower-contrast background
- **Tertiary actions** → styled as plain links

This reduces UI clutter and makes the primary path obvious, without hiding less-common actions.

### Destructive Actions

"Destructive" or "dangerous" doesn't automatically mean visually prominent. If deleting something is a rare, secondary action, it shouldn't look like a primary call-to-action just because it's red.

- If the destructive action is the primary action in a flow (e.g., a confirmation dialog that only exists to confirm deletion), make it the visually prominent button.
- If it's a secondary action alongside a primary one, de-emphasize it visually.

---

## Quick Reference: Hierarchy Signals

| Signal | When to use |
|--------|-------------|
| Large font + heavy weight | Absolute primary content (hero titles, key stats) |
| Normal font + heavy weight | Emphasized within body (subheadings, important labels) |
| Normal font + normal weight | Body content, standard text |
| Normal/small font + light color | Supporting text, metadata, secondary labels |
| Very light color | Tertiary, decorative, or placeholder text |
| Reduced opacity | Icons, decorative elements that should feel lighter |
