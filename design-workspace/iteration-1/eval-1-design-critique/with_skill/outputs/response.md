## Design Critique: SaaS Finance Dashboard — Overview Screen

### Overall Impression

The layout covers all the right content for a finance overview, but it stacks too many competing elements without a clear visual hierarchy — the large line chart dominates without enough context, and the data density risks overwhelming finance users who need to act fast, not just see data.

---

### Usability

| Finding                                                                                              | Severity    | Recommendation                                                                                                                       |
| ---------------------------------------------------------------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 8 sidebar nav items is at the high end of cognitive load — users can't scan it quickly               | 🟡 Moderate | Group related items under collapsible headers or reduce to 5–6 top-level items; move less-used items to a secondary menu or settings |
| KPI cards with no trend indicators make it impossible to know if numbers are good or bad at a glance | 🔴 Critical | Add a small sparkline or delta (e.g., "+12% vs last month") to each card; burn rate and runway especially need trend context         |
| Transactions table below the chart competes for attention without a clear entry point                | 🟡 Moderate | Limit the table to 5–7 rows with a "View all" link; de-emphasize it visually relative to the KPI row and chart                       |
| No clear primary action visible on the page                                                          | 🟡 Moderate | Finance users need quick actions (export report, add transaction, share). Add a primary CTA in the top nav or as a floating action   |

---

### Visual Hierarchy

- **What draws the eye first**: The line chart at 60% page width — this is likely wrong. KPIs (revenue, burn rate, runway) are more decision-critical and should anchor the eye first.
- **Reading flow**: Top nav → sidebar → KPI row → chart → table. The sidebar creates a left-pull that competes with the main content column on every page.
- **Emphasis**: The chart is over-weighted. Finance users glance at KPIs first; the chart provides detail on demand. Consider reducing chart height to ~35–40% and giving the KPI row more visual weight with larger numbers and bolder type.
- **Whitespace**: Data-dense layouts like this need deliberate section breathing room. If sections aren't clearly separated, the page reads as one undifferentiated block of information.

---

### Consistency

| Element                         | Issue                                                                                 | Recommendation                                                                                                    |
| ------------------------------- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| KPI cards vs transactions table | Two very different content densities in the same vertical flow with no visual divider | Add a section label and a subtle divider or background shift between regions                                      |
| Top nav + left sidebar          | Dual navigation creates ambiguity — which nav is for app-level context vs page-level? | Make their purposes explicit: top nav for account/settings/notifications, sidebar for page navigation only        |
| Chart sizing                    | 60% height is unlikely to match a consistent spacing scale                            | Constrain chart height to a defined token (e.g., 400px or 50vh max) so it behaves predictably across screen sizes |

---

### Accessibility

- **Color contrast**: Finance dashboards often use red/green for positive/negative values — ensure these are never the _only_ indicator (colorblind users). Pair with icons (▲▼) or labels ("up"/"down").
- **Touch targets**: Sidebar nav items need ≥44px touch targets if this is responsive/tablet-accessible.
- **Text readability**: KPI card numbers should be ≥24px bold; supplemental labels (card titles, table headers) should be ≥12px with sufficient contrast (≥4.5:1 for normal text).
- **Chart accessibility**: Line charts need accessible labels or a data table fallback for screen readers — SVG charts are often invisible to assistive tech without extra work.

---

### What Works Well

- The layout structure is logical: nav → summary → detail is the right information hierarchy in principle.
- Four KPI cards is an appropriate number for a summary row — it maps well to a 4-column grid and covers the key finance metrics.
- Putting the transactions table at the bottom treats it correctly as supporting detail rather than primary content.

---

### Priority Recommendations

1. **Give KPI cards more visual weight and add trend context** — Finance users arrive at this page to answer "are we on track?" The KPI row should be the dominant visual element with large numbers, color-coded deltas, and sparklines. Right now the chart overshadows the most decision-critical information.

2. **Reduce the chart to 35–40% height and add a section title** — The line chart is useful for trend analysis but shouldn't dominate the overview. Label it clearly ("Revenue vs Expenses — Last 12 Months"), shrink it, and let users expand or drill in if they need detail.

3. **Reduce sidebar to 5–6 items with grouping** — 8 top-level items is cognitively expensive for a tool finance teams use daily. Audit which items are used most; demote the rest. Consider a collapsed "More" or grouped headers (e.g., "Reports", "Settings") to reduce visual noise without removing functionality.
