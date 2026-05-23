# Flow Lens — Security & Data Handling Overview

**Document purpose:** This document describes how Flow Lens handles data and why it is safe to use with sensitive work management data.

---

## Summary

Flow Lens is a single, self-contained HTML file that runs entirely inside the user's web browser. It has no server, no backend, no network requests, and no data transmission of any kind. The CSV file you load into it never leaves your machine.

---

## What Flow Lens is

Flow Lens is a flow metrics tool for Kanban teams. The user downloads a single file (`flow-lens.html`) and opens it in any modern browser. They drag and drop a CSV export from their work management system, and the tool generates charts — cycle time, throughput, WIP, cumulative flow, and aging work items.

It is distributed as open-source software under the MIT licence. The source code is fully auditable at: https://github.com/Simeon-techbss/flow-lens

---

## Data handling

| Question | Answer |
|----------|--------|
| Is the CSV uploaded to any server? | No — read by the browser's File API into memory only |
| Is any data transmitted over the internet? | No — CSV data never leaves the device |
| Does the tool make any network requests? | No — fully self-contained, no external calls whatsoever |
| Is any data written to disk or browser storage? | No — no localStorage, cookies, or browser database writes |
| Is any data retained after closing the browser tab? | No — all data is discarded on tab close |
| Does the tool collect analytics or telemetry? | No — no analytics, no usage tracking, no error reporting |
| Can it be used offline? | Yes — always, with no setup required |

---

## Network activity

**Flow Lens makes zero automatic network requests.**

All JavaScript libraries are bundled directly inside the HTML file. Opening the tool does not contact any external server under any circumstances. No CDN, no internet connection required — ever.

The libraries embedded in the file are:

| Library | Purpose | Version |
|---------|---------|---------|
| Chart.js | Rendering charts | 4.4.0 |
| chartjs-adapter-date-fns | Date handling for charts | 3.0.0 |
| PapaParse | Parsing the CSV file | 5.4.1 |
| html2canvas | Screenshot export | 1.4.1 |

The only network activity the tool can produce is user-initiated: if the user clicks the link to the online guide or the author's website, those open in a new browser tab and carry no data.

---

## What does not happen

- No CSV data, work item titles, IDs, or dates are ever sent to any server
- No login, account, or registration is required
- No third-party analytics (Google Analytics, Mixpanel, etc.)
- No third-party advertising or tracking scripts
- No CDN or external library loading
- No server-side processing of any kind
- No persistent storage of any kind (cookies, localStorage, IndexedDB)

---

## Technical verification

Anyone with browser developer tools can verify these claims independently:

1. Open `flow-lens.html` in Chrome or Edge.
2. Open Developer Tools → **Network** tab.
3. Drop a CSV onto the page and interact with the charts.
4. Observe that zero network requests are made at any point.

All application logic is written in plain JavaScript within the single HTML file and is human-readable.

---

## Risk assessment

| Risk | Level | Notes |
|------|-------|-------|
| Data exfiltration to a remote server | None | No outbound data calls exist in the code |
| Data persisted on the user's machine | None | No storage writes of any kind occur |
| Supply chain compromise via CDN | None | No CDN used — libraries are bundled at fixed versions inside the file |
| Unauthorised access to the tool | None | No server, no login, and no shared instance |
| Data visible to other users | None | The tool runs locally in a single browser session only |

---

*Flow Lens is built and maintained by Simeon Herbert. MIT licence. For questions about this document contact simeon@techbss.co.uk.*
