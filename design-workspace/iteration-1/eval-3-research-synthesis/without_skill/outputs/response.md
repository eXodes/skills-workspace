# User Interview Synthesis — Project Management App

## Key Themes

### 1. Prioritization & Backlog Management

**Evidence:** P1, P6

Users struggle to understand what to work on next. The backlog lacks clarity, and there's no built-in way to surface blocked or high-priority items. Users resort to personal workarounds (custom labels, manual tags) to compensate.

### 2. Performance Issues in Complex Projects

**Evidence:** P2

The Gantt view degrades on large projects, forcing users to artificially constrain their view (2-week windows) to maintain usability. This is a functional workaround that limits visibility.

### 3. Search & Discoverability of Past Work

**Evidence:** P3

Search is not effective for historical lookup. Users fall back to browser history — an external tool — to find tasks they worked on previously. This signals that search either lacks recency weighting, filtering, or contextual relevance.

### 4. Notification Fatigue

**Evidence:** P4

Notifications are too noisy, causing users to disable them wholesale. This creates a secondary problem: missed deadlines. The system lacks granular notification controls or intelligent priority filtering.

### 5. Feature Accessibility / Paywall Friction

**Evidence:** P5

Core collaboration features (Gantt) are locked behind a paid tier. Users on free plans either can't access them at all or can't use them with their teams. This creates friction in collaborative workflows and may increase churn risk.

---

## Recommendations

### Short-term (High Impact, Lower Effort)

1. **"Focus View" or Daily Priority Surface** — Add a smart queue that surfaces what's most important next, accounting for blockers, deadlines, and dependencies. Directly addresses P1 and P6.

2. **Notification Preferences Granularity** — Allow users to configure notification types individually (e.g., deadline alerts only, @mentions only). Add a "mute all except critical" preset. Addresses P4.

3. **Search Improvements** — Add filters for date range, assignee, recent activity, and project. Surface recently-visited tasks. Addresses P3.

### Medium-term

4. **Gantt Performance Optimization** — Profile and optimize rendering for large datasets. Lazy-load tasks outside the current viewport. Addresses P2 without requiring workarounds.

5. **Blocked Status as First-Class Concept** — Make "blocked" a native task state with filtering, reporting, and notifications built in. Addresses P6 (and likely a broader unvoiced need).

### Strategic

6. **Revisit Paywall Tier Structure** — Consider making Gantt view available on free plans with limitations (e.g., read-only, or limited to N tasks), or introduce a free team tier. Blocking collaboration features behind payment risks losing entire teams. Addresses P5.

---

## Patterns Worth Noting

- **Workaround frequency is high**: 4 of 6 participants have built manual workarounds (labels, browser history, manual tags, date filters). This signals systemic gaps, not edge cases.
- **Two distinct user modes**: Some users work individually (P1, P3, P6), others are team-focused (P5). Recommendations should account for both.
- **Notification design is a trust issue**: Once users turn off notifications, re-engagement requires rebuilding that trust — a harder problem than getting it right initially.
