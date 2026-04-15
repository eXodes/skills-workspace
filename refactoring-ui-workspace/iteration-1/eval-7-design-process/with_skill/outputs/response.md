# UI Design Advice: Overcoming Decision Paralysis When Starting a New App

## Design Category: Design Process — Decision Fatigue

The paralysis you're feeling is a **systems problem**, not a taste problem. When you pick a font size or color from an unlimited pool of possible values, of course you'll second-guess yourself — the design space is infinite, and there's no principled way to feel confident. The fix is to stop picking individual values and start building constraints.

Here's the complete approach from Refactoring UI:

---

## 1. Don't Start With Colors or Font Sizes — Start With a Feature

**The problem with your current approach:** You're trying to make visual polish decisions before you have a design to polish. Colors and type scales are *finishing* decisions. They require something to apply them to.

**What to do instead:** Pick one real, concrete feature of your app — the main action a user comes to do — and design *just that*. Not the navigation shell, not the homepage, not the onboarding flow. One feature: a search form, a list view, a card, a modal.

This matters because an app is a collection of features. You don't have enough context to design global systems (navigation, layout) until you've designed at least one real piece of functionality.

---

## 2. Hold Color Entirely — Design in Grayscale First

**The principle: Detail Comes Later.**

Choosing colors before you have working structure is premature. Remove the variable entirely: design your first feature in black, white, and shades of grey only.

This forces you to create visual hierarchy using the tools that actually matter at this stage:
- **Spacing** — does the layout breathe correctly?
- **Size contrast** — does the heading clearly outrank the body text?
- **Weight contrast** — does the primary action stand out?

A grayscale design that works is far more valuable than a colorful design that's visually confused. Color is the easiest thing to add once structure is solid — and adding it to a well-structured grayscale layout takes minutes.

**Practical technique:** Sketch on paper with a thick Sharpie marker. It's physically impossible to obsess over details at that resolution. Generate 3–5 rough layouts quickly, then move to the screen with the one that makes the most structural sense.

---

## 3. Choose a Personality Before You Pick Anything

Before picking any color, font, or border radius, answer one question: **what personality should this app have?**

This is the single most important early decision, and it makes every subsequent decision faster. Rough guide from Refactoring UI:

### Font personality:
- **Serif typefaces** (Georgia, Playfair, etc.) → elegant, classic, trustworthy — good for editorial, legal, financial
- **Rounded sans-serifs** (Nunito, Poppins, etc.) → playful, friendly, approachable
- **Neutral sans-serifs** (Inter, DM Sans, etc.) → clean, modern — lets other elements carry the personality

### Color personality:
- **Blue** → safe, trusted, familiar (widely used in enterprise/productivity)
- **Gold/Yellow** → premium, sophisticated
- **Pink** → fun, friendly, less formal
- **Green** → natural, health-focused, financial
- **Dark/Black** → serious, high-end, formal

### Border radius:
- **No radius** → formal and serious
- **Small radius** → neutral, safe default
- **Large radius** → playful, friendly

You're not making final decisions here. You're **eliminating whole categories of options** so the remaining choices become manageable. Pick one word that describes the target personality ("trustworthy," "playful," "serious") and use it to filter.

---

## 4. Stop Picking Values — Define Systems

**This is the core fix for decision paralysis.**

The reason you second-guess every font size is that you're choosing from infinite possibilities. 12px? 13px? 14px? 15px? With no system, any of those feels equally right or wrong.

The solution: **define a constrained set of allowed values once**, then only pick from that set.

### Systems to define before you start designing:

| System | Example scale |
|---|---|
| **Font sizes** | 12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72px |
| **Font weights** | Regular (400), Medium (500), Semibold (600), Bold (700) |
| **Spacing/padding** | 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96px |
| **Border radii** | 2, 4, 6, 8, 16, 9999px (pill) |
| **Shadows** | sm, md, lg, xl (4 levels) |

You don't need all of these defined on day one. **Introduce each system the first time you make that category of decision**, then never make that low-level decision again — only choose from your defined values.

### How to use a system to stop second-guessing:

1. Make your best guess — e.g., "this heading should be 24px"
2. Compare it to the adjacent values in your scale (20px and 30px)
3. If 24px still looks best, you're done — move on
4. If 30px looks better, shift your comparison window: compare 30px vs 36px
5. Repeat once if needed, then commit

You're not searching infinite space anymore. You're doing binary elimination between 2–3 options. This is fast and produces confident decisions.

---

## 5. Don't Design Too Much Up Front

**The mistake:** Trying to solve every screen, every edge case, every state before building anything.

**What this causes:** You block yourself waiting to figure out "what if there are no results?" before you've even built the list view.

**The Refactoring UI approach:**
1. Design a *simple* version of the next feature
2. Build it
3. Hit real complexity → fix it in the working interface
4. Iterate until it works
5. Return to design mode for the next feature

Be a pessimist about scope: design the **smallest useful version** of each feature. A comment form without attachments still ships. A comment form that's blocked waiting to solve file attachments doesn't.

---

## Summary: The Anti-Paralysis Checklist

Before picking any colors or font sizes:

- [ ] **Pin the personality** — one word: playful, trustworthy, serious, friendly?
- [ ] **Choose one feature** to design first, not a full layout
- [ ] **Design in grayscale** — no colors until structure is working
- [ ] **Define your type scale** — 8–10 sizes, then only pick from those
- [ ] **Define your spacing scale** — a base-4 or base-8 scale works well
- [ ] **Work in cycles** — design → build → iterate, don't design everything up front

The second-guessing you feel isn't a sign that you lack taste. It's a sign you're making unconstrained decisions. Constraints are what make confident decisions possible.
