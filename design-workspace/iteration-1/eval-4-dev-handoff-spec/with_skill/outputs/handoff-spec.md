## Handoff Spec: Order Review Screen (Mobile Checkout)

### Overview

This is the final review screen before purchase confirmation in the mobile checkout flow. Users land here after entering shipping and payment details. The screen lets them verify their order, apply a promo code, and confirm purchase. High-stakes moment — errors or confusion here cause cart abandonment.

**User context:** User has already committed to buying; they're verifying, not browsing. Optimize for trust signals and a clear, confident CTA.

---

### Layout

Single-column scrollable layout. Fixed header and fixed CTA button. Scrollable middle section contains cart items and order summary.

```
┌──────────────────────────┐  ← Status bar
│ ← Back   Review your order│  ← Fixed header (NavigationBar)
├──────────────────────────┤
│                          │
│  [Cart Item]             │  ┐
│  [Cart Item]             │  │ Scrollable
│  [Cart Item]             │  │ content
│                          │  │ area
│  ─────────────────────── │  │
│  Order Summary           │  │
│  Subtotal       $XX.XX   │  │
│  Shipping       $X.XX    │  │
│  Tax            $X.XX    │  │
│  Total          $XX.XX   │  │
│                          │  │
│  ─────────────────────── │  │
│  [Promo code field]      │  ┘
│                          │
├──────────────────────────┤
│  [Place Order – $XX.XX]  │  ← Fixed CTA (above safe area)
└──────────────────────────┘  ← Home indicator / safe area
```

**Scroll behavior:** Only the middle section scrolls. Header and CTA button are sticky (do not scroll away). Bottom CTA sits above the device safe area inset.

**Safe area:** CTA container must respect `safeAreaInsets.bottom`. Add `padding-bottom: safeAreaInsets.bottom + spacing-md` to CTA wrapper.

---

### Design Tokens Used

| Token                     | Suggested Value             | Usage                                            |
| ------------------------- | --------------------------- | ------------------------------------------------ |
| `color-primary`           | Brand primary               | CTA button background, applied promo badge       |
| `color-primary-pressed`   | Primary darkened 12%        | CTA button active/pressed state                  |
| `color-surface`           | #FFFFFF                     | Screen background, card surfaces                 |
| `color-surface-secondary` | #F5F5F5                     | Order summary section background                 |
| `color-text-primary`      | #111111                     | Item names, total amount, headings               |
| `color-text-secondary`    | #666666                     | Qty, shipping label, tax label, subtotal label   |
| `color-text-inverse`      | #FFFFFF                     | CTA button label                                 |
| `color-text-disabled`     | #AAAAAA                     | Placeholder text in promo field                  |
| `color-border`            | #E0E0E0                     | Dividers, promo field border, item separators    |
| `color-error`             | #CC0000                     | Promo code error state border + message          |
| `color-success`           | #007A3D                     | Promo applied confirmation                       |
| `color-overlay`           | rgba(0,0,0,0.04)            | Pressed state overlay on list items              |
| `spacing-xs`              | 4px                         | Icon-to-text gap, tight inline spacing           |
| `spacing-sm`              | 8px                         | Between qty and price, between summary rows      |
| `spacing-md`              | 16px                        | Section padding, list item vertical padding      |
| `spacing-lg`              | 24px                        | Between major sections                           |
| `spacing-xl`              | 32px                        | CTA container top padding                        |
| `radius-sm`               | 4px                         | Promo input field corners                        |
| `radius-md`               | 8px                         | Cart item image, CTA button                      |
| `radius-lg`               | 12px                        | Order summary card                               |
| `font-heading-md`         | 18px / 600 / system         | Screen title "Review your order"                 |
| `font-heading-sm`         | 16px / 600 / system         | "Order Summary" section header                   |
| `font-body-md`            | 15px / 400 / system         | Item name, summary row labels                    |
| `font-body-sm`            | 13px / 400 / system         | Qty, secondary labels                            |
| `font-body-md-bold`       | 15px / 600 / system         | Price per item, total value                      |
| `font-cta`                | 17px / 600 / system         | CTA button label                                 |
| `shadow-sm`               | 0 1px 3px rgba(0,0,0,0.10)  | Sticky header bottom shadow                      |
| `shadow-md`               | 0 -2px 8px rgba(0,0,0,0.08) | CTA container top shadow (separates from scroll) |

---

### Components

| Component        | Variant                         | Props                                          | Notes                                                                                                                 |
| ---------------- | ------------------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `NavigationBar`  | default                         | `title="Review your order"`, `backAction`      | Fixed/sticky. Title centered. Back chevron + label left-aligned.                                                      |
| `CartItemRow`    | default                         | `image`, `name`, `qty`, `price`                | Repeated for each item. Tap opens item detail (optional — confirm with PM).                                           |
| `Divider`        | horizontal                      | —                                              | `color-border`, 1px, full-width, `spacing-md` vertical margin                                                         |
| `SectionHeader`  | —                               | `label`                                        | "Order Summary" label. `font-heading-sm`, `color-text-primary`.                                                       |
| `SummaryRow`     | default                         | `label`, `value`                               | Subtotal / Shipping / Tax rows.                                                                                       |
| `SummaryRow`     | total                           | `label="Total"`, `value`                       | Bold label + bold value. Slightly larger text (`font-body-md-bold`). Visually separated from above rows by a divider. |
| `PromoCodeField` | idle / active / applied / error | `value`, `onApply`, `onClear`, `errorMessage`  | See states table below.                                                                                               |
| `CTAButton`      | primary / loading / disabled    | `label`, `totalAmount`, `onPress`, `isLoading` | Full-width. Shows total in label: "Place Order · $XX.XX".                                                             |

---

### Cart Item Row Spec

```
┌─────────────────────────────────────┐
│ [img] Item Name                $XX.XX│
│       Qty: 2               [padding] │
└─────────────────────────────────────┘
```

| Property            | Value                                                           |
| ------------------- | --------------------------------------------------------------- |
| Image size          | 56×56pt                                                         |
| Image corner radius | `radius-md` (8px)                                               |
| Image aspect ratio  | 1:1 (square crop, `resizeMode: cover`)                          |
| Gap: image → text   | `spacing-sm` (8px)                                              |
| Item name           | `font-body-md`, `color-text-primary`, max 2 lines then ellipsis |
| Qty label           | `font-body-sm`, `color-text-secondary`, format: "Qty: {n}"      |
| Price               | `font-body-md-bold`, `color-text-primary`, right-aligned        |
| Row padding         | `spacing-md` vertical, `spacing-md` horizontal                  |
| Row height          | Variable (min 72pt)                                             |
| Tap feedback        | `color-overlay` pressed state                                   |

---

### Order Summary Section Spec

Background: `color-surface-secondary`. Corner radius: `radius-lg`. Margin: `spacing-md` horizontal. Padding: `spacing-md` all sides.

| Row      | Label      | Value format                   |
| -------- | ---------- | ------------------------------ |
| Subtotal | "Subtotal" | "$XX.XX"                       |
| Shipping | "Shipping" | "$X.XX" or "Free"              |
| Tax      | "Tax"      | "$X.XX"                        |
| Divider  | —          | 1px `color-border`, full-width |
| Total    | "Total"    | "$XX.XX" (bold)                |

Row height: 36pt. Vertical spacing between rows: `spacing-sm`.

---

### States and Interactions

#### Promo Code Field

| State            | Appearance                                                                                                           | Behavior                                                             |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Idle             | Border `color-border`, placeholder "Enter promo code", "Apply" text button right-aligned (color-text-secondary)      | Tapping field focuses it                                             |
| Active (focused) | Border `color-primary` 2px, "Apply" button activates                                                                 | Keyboard appears, field fills                                        |
| Applied          | Green checkmark icon + promo code text, "Remove" text button. Order summary updates to show discount row.            | "Apply" replaced by "Remove". Discount row appears in summary.       |
| Error            | Border `color-error` 2px, error message below field: "That promo code isn't valid." in `color-error` `font-body-sm`. | Message appears after failed apply attempt. Clears on next keypress. |
| Loading          | "Apply" button shows inline spinner, disabled                                                                        | While validating code server-side. Debounce 300ms before triggering. |

#### CTA Button

| State    | Appearance                                                     | Behavior                             |
| -------- | -------------------------------------------------------------- | ------------------------------------ |
| Default  | `color-primary` background, white label "Place Order · $XX.XX" | Enabled when order is valid          |
| Pressed  | `color-primary-pressed` background                             | 150ms transition                     |
| Loading  | Spinner replaces label text, button disabled                   | While order is being submitted       |
| Disabled | `color-text-disabled` background, dimmed label                 | If cart becomes empty or error state |

#### NavigationBar Back Button

| State | Behavior                                                                                                   |
| ----- | ---------------------------------------------------------------------------------------------------------- |
| Tap   | Navigate back to previous checkout step. Show confirmation dialog if order is in-progress (loading state). |

---

### Responsive Behavior

This is a mobile-first screen. No tablet or desktop breakpoints required for the initial sprint. Document breakpoints when web checkout is scoped.

| Breakpoint                    | Behavior                                                                                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Mobile portrait (<430pt wide) | Default layout as specced above                                                                                  |
| Mobile landscape              | Scrollable area height reduces. Header and CTA remain fixed. Ensure at least 2 cart items visible before scroll. |

---

### Edge Cases

- **Empty cart:** Should not reach this screen with an empty cart. If it somehow occurs (item removed server-side), show an inline error banner: "Some items in your cart are no longer available." with a "Review Cart" CTA replacing the Place Order button. Do not show a broken order summary.
- **Single item:** Layout unchanged. No minimum-item visual treatment needed.
- **Many items (10+):** List scrolls naturally. No pagination — render all items. If performance is a concern, implement windowed list (engineering decision).
- **Long item names:** Truncate at 2 lines with ellipsis (`numberOfLines={2}`). Full name accessible via tap (if item detail is in scope).
- **Long promo code strings:** Field clips overflow. Max input length: 32 characters.
- **"Free" shipping:** Show "Free" text in `color-success` in the Shipping value column, not "$0.00".
- **Zero tax:** Show "$0.00" — do not hide the row (avoids layout shift if tax gets added).
- **Large totals:** "$1,234.56" — ensure price columns have enough horizontal space. Right-align all price values.
- **Promo removes all shipping:** Discount row appears in summary. Shipping row shows "Free".
- **Slow network on Place Order:** CTA enters loading state immediately on tap. If request exceeds 8s, show a non-blocking toast: "Still processing your order…" Do not allow double-tap (button disabled while loading).
- **Network error on Place Order:** Show full-screen error state or inline banner (coordinate with error handling team): "Something went wrong. Your card was not charged." with a "Try Again" action.
- **Network error on promo apply:** Promo field shows error state: "Couldn't verify code. Please try again."

---

### Animation / Motion

| Element                 | Trigger       | Animation                                           | Duration       | Easing   |
| ----------------------- | ------------- | --------------------------------------------------- | -------------- | -------- |
| CTA button pressed      | onPressIn     | Background color → `color-primary-pressed`          | 150ms          | ease-out |
| CTA button release      | onPressOut    | Background color → `color-primary`                  | 100ms          | ease-in  |
| Promo field focus       | onFocus       | Border color transition to `color-primary`          | 200ms          | ease     |
| Promo error message     | onError       | Fade in + slide down 4px                            | 200ms          | ease-out |
| Promo applied           | onSuccess     | Checkmark fade in, discount row slides into summary | 250ms          | ease-out |
| Discount row in summary | promo applied | Height from 0 → natural, opacity 0 → 1              | 300ms          | ease-out |
| CTA loading spinner     | onSubmit      | Fade out label, fade in spinner                     | 150ms          | ease     |
| Keyboard appearance     | field focus   | CTA button and summary scroll up to stay visible    | System-managed | System   |

**Reduce Motion:** When `prefers-reduced-motion` / `reduceMotionEnabled` is true, skip all transitions. Apply state changes immediately with no animation.

---

### Accessibility Notes

**Focus order (top to bottom):**

1. Back button
2. Screen title ("Review your order") — `accessibilityRole="header"`
3. Each cart item row (announced as: "{Item name}, Qty {n}, ${price}")
4. Order summary section header ("Order Summary") — `accessibilityRole="header"`
5. Each summary row (announced as: "{Label}: {Value}")
6. Promo code text input (`accessibilityLabel="Promo code"`)
7. Apply / Remove button
8. Place Order button

**ARIA / Accessibility labels:**

| Element            | Label                                                                                          |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| Back button        | "Go back"                                                                                      |
| Cart item row      | "{name}, quantity {qty}, {price}"                                                              |
| Image in cart item | `accessibilityElementsHidden={true}` (decorative)                                              |
| Promo field        | `accessibilityLabel="Promo code"`                                                              |
| Apply button       | "Apply promo code"                                                                             |
| Remove button      | "Remove promo code {code}"                                                                     |
| Promo error        | `accessibilityLiveRegion="assertive"` — announce error immediately                             |
| Promo success      | `accessibilityLiveRegion="polite"` — announce discount applied                                 |
| CTA button         | "Place order, total {totalAmount}"                                                             |
| CTA loading        | `accessibilityLabel="Placing your order, please wait"` + `accessibilityState={{ busy: true }}` |

**Keyboard / External keyboard (iOS/Android):**

- Tab through all interactive elements in focus order above
- Enter / Space activates focused button
- Escape closes keyboard if field is focused

**Minimum tap targets:** All interactive elements ≥ 44×44pt.

**Color contrast:**

- Body text on white background: meets AA (≥ 4.5:1)
- CTA button text on primary: must meet AA — verify with final brand color
- Error text `color-error` on white: must meet AA
- Secondary text `color-text-secondary` (#666666 on #FFFFFF): 5.74:1 — passes AA

---

### Implementation Notes

- Scaffold as a single `ScrollView` with `stickyHeaderIndices` or a `FlatList` with a `ListHeaderComponent` (order summary + promo) and `ListFooterComponent` — discuss with mobile engineer.
- CTA button is not inside the scroll view. It sits in a sibling `View` with absolute or flex positioning.
- Order totals must be computed client-side optimistically and re-fetched/validated server-side on Place Order tap (do not trust client total for billing).
- Promo code validation is server-side only. Client shows loading state during request.
- If using a `FlatList`, add `keyExtractor` on item ID, not index (items can be removed).
