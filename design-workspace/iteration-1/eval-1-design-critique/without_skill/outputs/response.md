# Eval 1: Design Critique — Baseline Response (No Skill)

**Prompt:** I'm building a SaaS dashboard for finance teams. Here's our main overview screen: a top nav with logo + avatar, a left sidebar with 8 nav items, a summary row of 4 KPI cards (revenue, expenses, burn rate, runway), then a large line chart taking up 60% of the page, and below that a transactions table. The whole thing is pretty data-dense. Can you critique this layout?

---

## Response

This is a common layout pattern for financial dashboards, and it has some solid structural choices but also a few areas worth addressing.

**What works**

- Top nav + left sidebar is a well-established pattern users expect in SaaS tools. It gives persistent navigation without eating content space.
- KPI cards in a summary row give quick at-a-glance status, which is exactly right for an overview screen.
- Putting the chart before the table follows natural information hierarchy: trend first, then detail.

**Issues and recommendations**

**1. Left sidebar with 8 nav items is too many for an overview screen**

Eight items suggests the app has grown without pruning. Finance users typically have 2-3 core jobs: monitoring, reporting, and managing. Group items into sections with headers (e.g., "Monitor", "Reports", "Settings") or use a collapsible sidebar with icons + labels. A flat list of 8 creates cognitive load before the user even reaches the content.

**2. The line chart at 60% of the page is likely too large**

60% is a significant real estate allocation. Ask: what decision does this chart support? If users glance at it to confirm a trend, a smaller chart (30-40%) with the ability to expand is more appropriate. If they actively analyze it, consider making it the primary focus with the KPI cards moved to a sidebar panel. At 60%, you may be solving for "impressive" rather than "useful."

**3. KPI card row needs hierarchy within itself**

Four cards side by side at equal weight compete with each other. Burn rate and runway are typically the most critical for finance teams—they're time-sensitive. Consider making those two visually heavier (larger number, accent color) or leading with them on the left.

**4. The transactions table below the chart will be below the fold**

With a top nav, a sidebar, a KPI row, and a 60% chart, the transactions table is almost certainly not visible on initial load. Users will need to scroll to reach it. This is fine if it's secondary content, but if finance teams actually use the table frequently (they usually do—reconciliation, auditing), you're burying a core workflow. Options:

- Reduce the chart height
- Make the table collapsible/expandable
- Move the table to its own tab or sub-page

**5. Data density is a design choice, not a problem—but needs typographic discipline**

Dense dashboards are legitimate for power users. The risk is that everything reads at the same visual weight. Apply strict typographic hierarchy: primary numbers large and bold, labels small and muted, secondary metadata in a lighter color. Use consistent spacing tokens rather than letting content stack up. Whitespace is not waste—it's what makes the numbers legible at a glance.

**Summary**

The structural skeleton is sound but needs tuning on hierarchy, allocation, and scroll behavior. The two highest-priority changes are: (1) shrink the chart to free vertical space for the table, and (2) establish visual hierarchy within the KPI row so the most critical metrics lead.
