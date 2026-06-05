# Dev Handoff Spec: Order Review Screen

**Screen:** Order Review (Checkout Flow)
**Platform:** Mobile (iOS + Android)
**Sprint:** Next sprint

---

## Overview

This is the final review screen before payment. Users confirm their order before submitting.

---

## Screen Structure

```
┌─────────────────────────────┐
│  [Back]   Review your order │
├─────────────────────────────┤
│                             │
│  ┌─────────────────────┐    │
│  │ [img] Item name     │    │
│  │       Qty: 1  $9.99 │    │
│  └─────────────────────┘    │
│  ┌─────────────────────┐    │
│  │ [img] Item name     │    │
│  │       Qty: 2 $19.99 │    │
│  └─────────────────────┘    │
│  ... (scrollable)           │
│                             │
│  ─────── Order Summary ─────│
│  Subtotal          $29.98   │
│  Shipping           $4.99   │
│  Tax                $2.40   │
│  ─────────────────────────  │
│  Total             $37.37   │
│                             │
│  ┌─────────────────────┐    │
│  │  Promo code    [Apply]   │
│  └─────────────────────┘    │
│                             │
├─────────────────────────────┤
│  [     Place Order     ]    │
└─────────────────────────────┘
```

---

## Components

### 1. Header

| Property    | Value                                    |
| ----------- | ---------------------------------------- |
| Title       | "Review your order"                      |
| Style       | Navigation bar / top app bar             |
| Back button | Yes — navigates to cart or previous step |

---

### 2. Cart Items List (Scrollable)

**Container:** Vertically scrollable list. Scroll region excludes the sticky header and sticky CTA.

**Each cart item row:**

| Element       | Description                                       |
| ------------- | ------------------------------------------------- |
| Product image | Square thumbnail, rounded corners                 |
| Product name  | 1–2 lines, truncate with ellipsis if overflow     |
| Quantity      | Displayed as "Qty: N" (read-only on this screen)  |
| Price         | Right-aligned, line item total (unit price × qty) |

**States:**

- Default
- Long product name (truncation)
- Multiple items (scroll)

---

### 3. Order Summary Section

Displayed below the cart items list (not sticky — scrolls with content).

| Line Item | Notes                                               |
| --------- | --------------------------------------------------- |
| Subtotal  | Sum of all line items                               |
| Shipping  | Flat rate or calculated — show "Free" if applicable |
| Tax       | Calculated based on address                         |
| Divider   | Horizontal rule above Total                         |
| **Total** | Bold, larger font than other rows                   |

---

### 4. Promo Code Field

| Property      | Value                                             |
| ------------- | ------------------------------------------------- |
| Input         | Text field, placeholder: "Enter promo code"       |
| CTA           | "Apply" — inline button or text button            |
| Success state | Show discount applied, update summary totals      |
| Error state   | Inline error message below field ("Invalid code") |
| Keyboard      | Dismisses on Apply or outside tap                 |

---

### 5. Primary CTA Button (Sticky)

| Property      | Value                                                               |
| ------------- | ------------------------------------------------------------------- |
| Label         | "Place Order"                                                       |
| Position      | Fixed to bottom, above safe area / home indicator                   |
| Style         | Full-width primary button                                           |
| States        | Default, Loading (spinner), Disabled                                |
| Disabled when | … not applicable by default; always enabled unless validation fails |

---

## Layout & Spacing

| Token                     | Value                                        |
| ------------------------- | -------------------------------------------- |
| Screen horizontal padding | 16px                                         |
| Cart item row height      | ~80px (image 56px + 12px padding top/bottom) |
| Image size                | 56×56px                                      |
| Image corner radius       | 8px                                          |
| Row separator             | 1px divider or 8px gap                       |
| Section spacing (summary) | 24px top margin from last cart item          |
| Promo field top margin    | 16px from summary total                      |
| CTA bottom padding        | 16px + safe area inset                       |

---

## Typography

| Element           | Style                             |
| ----------------- | --------------------------------- |
| Screen title      | Heading / H1 — ~18–20px, semibold |
| Product name      | Body — ~14–16px, medium           |
| Qty + price       | Caption/body — ~12–14px, regular  |
| Summary labels    | Body — ~14px, regular             |
| Total label/value | Body — ~16px, bold                |
| CTA label         | Button — ~16px, semibold          |

---

## Colors (Use Design Token Names)

| Element             | Token                               |
| ------------------- | ----------------------------------- |
| Background          | `surface.primary`                   |
| Header background   | `surface.nav`                       |
| Item row background | `surface.card` or `surface.primary` |
| Divider             | `border.subtle`                     |
| CTA background      | `color.primary`                     |
| CTA label           | `color.on-primary`                  |
| Error text          | `color.error`                       |
| Total text          | `content.primary`                   |

---

## Scroll Behavior

- Header: sticky at top
- CTA: sticky at bottom
- Content between header and CTA: scrollable (cart items + summary + promo)
- Scroll does not affect header or CTA position

---

## Edge Cases & States

| Scenario                           | Behavior                                                |
| ---------------------------------- | ------------------------------------------------------- |
| Single item in cart                | No scroll needed; layout fits screen                    |
| Many items                         | Scroll enabled; summary + promo visible after scrolling |
| Long product name                  | Truncate at 2 lines with ellipsis                       |
| Promo applied                      | Discount line appears in summary; total updates         |
| Invalid promo                      | Inline error below field; totals unchanged              |
| Free shipping                      | Show "Free" instead of "$0.00"                          |
| Loading state (Place Order tapped) | CTA shows spinner; disable tap                          |
| Network error                      | Show error toast/snackbar                               |

---

## Accessibility

- All interactive elements have accessible labels
- CTA minimum tap target: 44×44px
- Color is not the sole indicator of state (use icons/text alongside color)
- Product images have `alt` text (product name)
- Screen reader reading order: Header → Cart items → Summary → Promo → CTA

---

## Interactions & Navigation

| Action          | Result                                                          |
| --------------- | --------------------------------------------------------------- |
| Back button tap | Navigate to previous checkout step / cart                       |
| Apply promo     | Validate code; update totals or show error                      |
| Place Order tap | Show loading state → navigate to confirmation screen (or error) |

---

## Assets Needed

- Product thumbnail images (from cart data, not static assets)
- Back arrow icon
- Loading spinner (system default or design system component)

---

## Notes for Dev

- Totals should be formatted with currency symbol and 2 decimal places
- Promo code field should auto-trim whitespace before API call
- Use real cart data from state/store — do not hard-code values
- Price display: show unit price × qty as line total
- Sticky footer CTA must respect safe area insets (iOS notch / Android nav bar)
