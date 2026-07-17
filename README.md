# Korognai SMO — Reference Implementation

A single self-contained HTML file that simulates a Service Management & Orchestration (SMO) platform for mobile networks — built as a hands-on portfolio/interview piece, not a product. No build step, no backend, no external dependencies at runtime: open `index.html` in a browser and it runs, entirely on synthetic, in-browser data.

This deliverable actually ships **two** linked experiences in one file:

1. **Korognai SMO (RAN)** — the main site. A RAN-focused SMO/Non-RT RIC reference implementation: architecture, FCAPS, closed-loop rApps, slicing, security, and documentation.
2. **Cross-Domain SMO — concept preview** — a forward-looking companion build that extends the same patterns across **RAN + Core + Transport**, reachable from the main site via the pulsing **"Want to see into the future?"** card next to the header. It opens in an isolated in-page overlay (an iframe), so its own tabs, data, and scripts never collide with the main RAN app.

Everything in both experiences is simulation: alarms, KPIs, topologies, and scenarios are synthetic, generated in-browser. Nothing here is live network data, and no vendor's proprietary material is used anywhere in it.

---

## Quick start

Just open `index.html` in any modern browser. That's it — no `npm install`, no server, no build.

## What's inside — Korognai SMO (RAN)

| Tab | What it shows |
|---|---|
| Overview | Plain-language landing page, executive KPIs, clickable functional clusters |
| RAN Architecture | Interactive RU/DU/CU diagram with the full O1/O2/A1/E2/F1/E1 interface map |
| FCAPS Monitor | Live fault, performance, configuration, trace, and topology/inventory views |
| Closed Loop | Multi-vendor cell ring + 10,000-cell fleet view, driven by 6 real rApps (ESM, ANR, MRO, MLB, COC, PCI) with one-to-one trigger scenarios |
| Near-RT RIC | The fast (10ms–1s) E2 control loop and xApps, contrasted against the Non-RT RIC |
| rApp Catalog | Toggleable rApps, each running genuine reference logic |
| Import rApp | Validate & onboard a new rApp via JSON descriptor (genuine logic for known algorithms, honest stub otherwise) |
| Slice Lifecycle | Full NSSI lifecycle (Create → Modify → Monitor & Assure → Decommission) with SLA-vs-intent visualization |
| Conflict Log | Live rApp-vs-rApp conflict detection with 3 resolution strategies (Allow / FCFS / Priority-Based Override) |
| Data & Openness | Data coverage matrix, disconnect/reconnect resilience simulator, self-serve data routing |
| Cloud & NF Lifecycle | 100-object live infrastructure inventory: Instantiate / Heal / Scale / Upgrade / Terminate |
| Zero-Touch Rollout | 13-step governed commissioning pipeline: onboard → discover → deploy → commission → validate → audit |
| Security & Trust | Evidence-based security posture + live supply-chain artifact verification |
| Openness Scorecard | Six industry principles, live-computed from actual demo state, freely adjustable |
| Documentation | Full glossary, tab-by-tab guide, scenario reasoning, design principles, acronym index |
| 50 Design Questions | 224 public-standards-based questions mapped to exactly where this demo answers each one |

## What's inside — Cross-Domain SMO (concept preview)

Same philosophy, extended to all three managed domains under one control plane, with a reorganized nav: top-level cross-domain tabs, plus three domain dropdowns (**RAN & Apps**, **Core & Apps**, **Transport & Apps**) that each mirror the same pattern — Architecture, App Catalog, Import App, Data & Openness, Cloud & NF Lifecycle.

| Tab | What it shows |
|---|---|
| Overview | Cross-domain executive summary and functional clusters |
| Cross-Domain Topology | Where SMO/Non-RT RIC sits over RAN, transport and core; the interfaces that tie it together (TAPI, TS 28.312 intent, Nnwdaf, Non-RT RIC Federation, CAMARA/Open Gateway, SEPP) |
| Cross-Domain Loop | RAN closed loop (cell ring + 6 rApp triggers) + Core closed loop (5 cApp triggers) + Transport closed loop (5 tApp triggers) + a worked cross-domain SLA-breach scenario — each with a Technical/Plain-language (Copilot) log toggle |
| Cross-Domain Conflict | Same-domain conflict resolution for RAN, Core, and Transport individually, **plus** a fourth section simulating true cross-domain conflict (one domain's fix undermining another's) |
| RAN & Apps *(dropdown)* | RAN Architecture, Near-RT RIC, rApp Catalog, Import rApp, Slice Lifecycle, Data & Openness, Cloud & NF Lifecycle, Zero-Touch Rollout, 50 Design Questions |
| Core & Apps *(dropdown)* | Core Architecture (5GC SBA diagram + function/interface reference), App Catalog (5 cApps), Import App, Data & Openness, Cloud & NF Lifecycle |
| Transport & Apps *(dropdown)* | Transport Architecture (fronthaul/midhaul/backhaul + T-SDN diagram + function/interface reference), App Catalog (5 tApps), Import App, Data & Openness, Cloud & NF Lifecycle |
| FCAPS Monitor | Cross-domain FCAPS summary, plus unified Fault/Performance/Configuration feeds — equal counts (20 each) across RAN, Core and Transport |
| Security & Trust | Same evidence-based posture, now including Core/Transport artifacts and a cross-domain interface security control |
| Openness Scorecard | Same six principles, "Trustworthy automation" now scored across rApps **and** cApps **and** tApps together |
| Future & Standards Radar | Honest L0–L5 autonomy self-placement (currently L4, high autonomy) and a forward-looking radar: AI-native RAN, 6G/IMT-2030, network digital twins, Non-RT RIC Federation, intent-based management, GSMA Open Gateway/CAMARA, energy standardization, post-quantum-ready O-RAN security |
| Documentation | Rebalanced glossary (RAN + Core + Transport + cross-domain/standards sections), tab-by-tab guide, scenario reasoning for all three domains, design principles, a 70-term acronym index |

### The two automation app families

- **rApps** — RAN domain, run on the Non-RT RIC (the original O-RAN pattern)
- **cApps** — Core domain, subscribe to NWDAF/SBI telemetry, act via core network function provisioning
- **tApps** — Transport domain, subscribe to TAPI/PTP telemetry, act via the T-SDN controller

All three follow the identical detect → decide → act closed-loop pattern, each with a real catalog, import flow, and conflict-resolution logic.

## Design principles this demo tries to hold itself to

- **Honesty over polish** — synthetic data is labeled as such throughout; gaps and limitations are called out rather than hidden.
- **Public-standards-only sourcing** — grounded in O-RAN Alliance, 3GPP, TM Forum, ETSI, ITU, ONF, GSMA, NIST and CIS material; no vendor-internal or proprietary content.
- **Genuine logic where it matters** — the rApp/cApp/tApp closed loops run real reference algorithms, not scripted animations; conflicts are detected live, not staged.
- **Practitioner voice** — written the way a working solution architect would explain it to a colleague, not marketing copy.

## Tech notes

- Single HTML file per experience; no framework, no build step, no server.
- The Cross-Domain concept is embedded in the main file as a base64-encoded payload and rendered into an isolated `<iframe>` on demand (via the "Want to see into the future?" card), which keeps its element IDs and JS globals from colliding with the main RAN app's.
- All charts, diagrams and tables are hand-rolled SVG/HTML/CSS — no charting library dependency.

## Author

Janos (Kornel) Korognai — 21 years in telecom pre-sales and solution architecture (OSS, network management, SMO, Non-RT RIC, rApps, O-RAN) for Tier-1 operators. This is an independent, hands-on project built to demonstrate the concepts hands-on, not affiliated with or endorsed by any vendor.
