# Flow Lens

Single-file HTML flow metrics tool. No server, no build step — everything is in `flow-lens.html`. Open it in a browser and drop a CSV.

## What it does

Analyses Actionable Agile CSV exports from ServiceNow. Each workflow stage has its own column containing the date the item entered that stage.

**Tabs:** Flow Insights, Control Chart, Throughput, WIP Over Time, CFD, Histogram, Aging WIP, Data

## Key technical decisions

**Date detection** — strict regex only, no `new Date()` fallback. Edge/Chromium is permissive and will parse "Title" as a date. Full row scan (not sample) so sparse columns like "Not done" are detected correctly.

**CFD calculation** — "reached this stage or further" approach: each line = items that entered that stage OR any later stage. This guarantees non-negative bands even when items skip stages in the data (common in ServiceNow test data). Do not revert to simple cumulative-entered counts.

**CFD stacking** — `fill: '-1'` in Chart.js, NOT `stacked: true`. Reversed dataset order (Done at bottom, To do at top). Traditional CFD convention.

**Aging WIP chart** — scatter chart with x = workflow stage (numeric index), y = age in days. Percentile bands drawn via inline Chart.js plugin (`agingBandPlugin`). `currentStage` set in `processData` by scanning `workflowStages` in reverse.

## Workflow column order (Simeon's data)

`To do → Doing → Ready for validation → Validation → Done → Not done`

"Not done" is a closed/cancelled terminal state, NOT completion. Don't treat it as an end date.

## Libraries (all CDN, no npm)

- Chart.js 4.4.0
- chartjs-adapter-date-fns 3.0.0
- PapaParse 5.4.1

## Data quirks (test data)

- 452 completed items all have 0-day cycle time (Doing and Done are same date) — histogram shows empty state, this is correct
- "Doing" band in CFD is nearly invisible (~5 items) — correct, reflects the data
- Items regularly skip stages — handled by the CFD calculation above
