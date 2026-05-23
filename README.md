# Flow Lens

A browser-based flow metrics tool for Kanban teams. Drop in a CSV, get instant charts — no installation, no server, no data leaving your machine.

## Download and use

**[Download flow-lens.html](flow-lens.html)** · open it in any modern browser · drop your CSV in.

That's it. No sign-up, no cloud, no dependencies to install.

## What it shows

| Tab | What it tells you |
|-----|-------------------|
| Flow Insights | Cycle time percentiles (p50/p70/p85/p95) and throughput summary |
| Control Chart | Cycle time scatter plot with percentile lines — spot outliers |
| Throughput | Weekly completion rate bar chart |
| WIP Over Time | Work in progress by week |
| CFD | Cumulative Flow Diagram — identify bottlenecks and flow problems |
| Histogram | Cycle time distribution |
| Aging WIP | Items in progress and how long they've been there |
| Data | Full item table with filtering |

## What CSV it needs

One row per work item. One column per workflow stage containing the date the item entered that stage. Empty cell = item hasn't reached that stage.

**[Full data format guide →](guide.html)**

Quick example:

| ID | Title | To do | Doing | Review | Done |
|----|-------|-------|-------|--------|------|
| T-1 | Fix login bug | 2026-01-10 | 2026-01-13 | 2026-01-14 | 2026-01-15 |
| T-2 | Add export | 2026-01-11 | 2026-01-14 | | |

Column names don't matter — you map them inside the tool. Works with any system that can export a date-per-stage CSV.

## Libraries used

All loaded from CDN — no npm, no build step.

- [Chart.js 4.4.0](https://www.chartjs.org/)
- [chartjs-adapter-date-fns 3.0.0](https://github.com/chartjs/chartjs-adapter-date-fns)
- [PapaParse 5.4.1](https://www.papaparse.com/)

## Licence

MIT — see [LICENSE](LICENSE)
