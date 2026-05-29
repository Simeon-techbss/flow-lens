# Vacanti Feature Suggestions for Flow Lens

Based on review of *Actionable Agile Metrics for Predictability* and *When Will It Be Done?* by Daniel Vacanti.

Already well covered: Monte Carlo (How Many + When), SLE/85th percentile, Little's Law, CFD, CT histogram, throughput, WIP over time, aging WIP, flow efficiency, started vs completed demand comparison.

---

## ✅ Done

**XmR / Normal Range on Throughput**
Toggle on throughput chart showing upper/lower normal range band (XmR calculation). Bars outside the range highlighted orange. Interpretation panel with variability rating (Low/Moderate/High) and plain-English signal list. Low-throughput guard (<5 items/week) to avoid misleading "High variability" on integer data.

**Throughput Histogram**
Second chart card on the Throughput tab showing frequency distribution of weekly throughput. Bars shaded by proximity to mean (brighter = near average). Info panel explaining what the shape means for forecasting reliability.

**Blocker Impact on Cycle Time**
The stat cards already show p50/p85/p95 for blocked vs not-blocked clearly — a chart adds no value. Not implemented.

---

## Backlog

### 2. SLE Stability Over Time
*Priority: Medium*

A line chart showing the 85th percentile cycle time across rolling time windows (e.g. each month or quarter). Flat or falling = predictability improving. Rising = system degrading.

Why: The Team Health tab compares current vs previous period (one comparison). A time series shows drift that a single period comparison misses. Teams often don't notice slow degradation until it's a crisis. X = month/quarter, Y = 85th percentile CT in days.

---

### 3. ✅ Classes of Service — Breakdown tab
*Implemented as a general Breakdown tab (split by any categorical column)*

Table showing items done, throughput/wk, CT p50, CT p85, blocked %, and WIP now per category. Exclusion filters respected; slice filters ignored (with a notice explaining which). Mini inline bars for visual comparison. Companion feature: global filter context bar showing active filters as chips on all tabs.

---

### 4. CFD Anti-Pattern Detection
*Priority: Low-medium*

Automated text callouts below the CFD when known problem patterns are detected:
- Widening bands → WIP is growing
- Flat horizontal area → throughput has stalled (bottleneck)
- Step pattern → work is being batched rather than flowing continuously

Currently the CFD renders correctly but doesn't coach the reader. Would be similar to the Team Health signals already implemented.

---

*Last updated: 2026-05-29*
