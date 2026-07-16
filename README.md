# Korognai SMO — Reference Implementation

A self-contained, browser-based reference demo of a Service Management & Orchestration (SMO) platform for O-RAN networks — built to show, not just describe, how FCAPS assurance, multi-vendor RAN integration, cloud & lifecycle automation, closed-loop rApp orchestration, Near-RT RIC/xApp control, network slicing, and security posture actually fit together in one platform.

🔗 **Live demo:** http://smo.korognai.net
🔗 **Repo:** https://github.com/yoroyarell/smo-demo

---

## Why this exists

Presales and solution-architecture conversations often need a working demonstration on short notice — a way to *show* a platform's value instead of describing it from a slide. This project turns that idea into a single, dependency-free HTML file that runs entirely in the browser: no backend, no build step, no server to keep alive during a live conversation.

Everything on screen is real industry-standard practice (O-RAN, 3GPP, TM Forum, NIST, CIS) applied to **synthetic, in-browser telemetry** — there is no live network behind this, and no vendor's proprietary data or code is used anywhere in it.

## What's inside

| Tab | What it shows |
|---|---|
| **Overview** | Plain-language landing page grouping every function into 8 domains, with executive-facing KPIs (OPEX saved, issues auto-resolved, MTTR) |
| **RAN Architecture** | Interactive RU/DU/CU diagram with the full O1/O2/A1/E2/F1/E1/O-FH interface map — hover any interface, in either the diagram or the reference table, to highlight it in both at once |
| **FCAPS Monitor** | Live fault, performance, configuration, trace, and topology/inventory views. Four scrollable panels sharing one consistent box size: 100 active alarms (independent Acknowledge and Cancel actions), 10 live KPIs (hover any one for a synthetic 24h trend plus its min/max, clearly labeled as illustrative), 100 configuration-change entries, and trace sessions (hover a completed one for a synthetic trace analysis snapshot) |
| **Closed Loop** | Multi-vendor cell ring (12-cell sample + a 10,000-cell fleet heatmap) driving real O-RAN SON algorithms across all 6 rApps — Energy Saving Management, Automatic Neighbor Relation, Mobility Robustness Optimization, Mobility Load Balancing, Cell Outage Compensation, and PCI Reuse Optimization — all enabled by default. Six color-coded buttons inject one condition each, matched to the rApp that resolves it, with a visible cyan pulse on the affected cell. If two enabled rApps genuinely want to act on the same cell in the same cycle, that's a real detected conflict, logged live to Conflict Log |
| **Near-RT RIC** | The fast (10ms–1s) control loop over E2, running xApps — deliberately contrasted against the slower Non-RT RIC loop on Closed Loop |
| **rApp Catalog** | Toggleable rApps with real reference logic, each showing which R1 services it consumes |
| **Import rApp** | Validates and onboards a JSON rApp descriptor (O-RAN R1-style schema), running genuine logic for recognized algorithms and an honest monitoring-only stub for anything else |
| **Slice Lifecycle** | Full NSSI lifecycle (create → modify → monitor/assure → decommission) plus SLA-vs-intent visualization. Each stage documents exactly what input it needs and where that input would come from in a real deployment — an operator intent, a formal OSS/BSS order, a closed-loop rApp recommendation, or a service-termination trigger |
| **Conflict Log** | Live rApp-vs-rApp conflict detection and resolution (Allow / First-Come-First-Served / Priority-Based Override), fed both by a manual "simulate a conflict" button and by genuine conflicts detected automatically on the Closed Loop tab |
| **Data & Openness** | Data coverage matrix, a disconnect/reconnect resilience simulator, and self-serve data-routing config |
| **Cloud & NF Lifecycle** | A live, scrollable, 100-object infrastructure inventory. Click any object to select it, then Instantiate / Heal / Scale / Upgrade / Terminate — the other four actions operate on whichever object is selected (Heal only does something if it's actually degraded). Status drifts on its own over time — an object can spontaneously degrade, and any transient state (scaling/upgrading/healing/instantiating) settles back to normal on its own after a while, so nothing stays stuck |
| **Zero-Touch Rollout** | A 13-step governed commissioning pipeline (onboard → discover → deploy → commission → validate → audit), with a note on exactly where a new integration's data comes from: the artifact registry, O1 Plug-and-Play hardware discovery, planning-tool site templates, and the shared PM feed for post-launch validation |
| **Security & Trust** | Evidence-based security posture (zero-trust, CIS hardening, supply-chain integrity) with a live artifact-verification log that explains what each check actually does and how the next artifact is selected (a round-robin queue, not random) |
| **Openness Scorecard** | Six industry-standard evaluation principles, each pre-populated from real state elsewhere in the demo and freely adjustable, with documentation on exactly which action on which tab moves each score and how manual slider overrides interact with the recalculate button |
| **Documentation** | A full written glossary, acronym index, tab-by-tab guide, scenario reasoning, and design-principles writeup — everything needed to understand the demo without a live walkthrough |
| **50 Design Questions** | A public-standards-based series of 50 design questions (224 specific sub-questions total, grouped into 8 themes) for evaluating any SMO platform, each showing exactly where — and how honestly — this demo answers it, gaps included |

Hover any jargon term throughout the demo (tab names, KPI titles, abbreviations) for a plain-English explanation — the whole thing is built to be equally readable by an engineer and a VP.

## Design choices worth knowing

- **One file, no backend.** Everything — UI, simulation logic, telemetry generation — lives in `index.html`. Nothing depends on a live connection, which matters when you're demoing in a room with unreliable wifi.
- **Honest about synthetic data.** Every screen is clearly marked as simulation. Imported rApps that don't match a recognized algorithm are labeled as monitoring-only stubs rather than silently pretending to run real logic.
- **Grounded in public standards, not vendor lock-in.** Terminology and behavior are drawn from O-RAN Alliance, 3GPP, TM Forum, ETSI, NIST, and CIS public material — no proprietary vendor documentation, confidential material, or trademarked product names are used anywhere in this repo.
- **Scales in the way real tools scale.** The Closed Loop tab includes both a 12-cell interactive sample and a 10,000-cell aggregated heatmap, to make the point that dashboards need aggregation + drill-down at scale, not one dot per cell.
- **Real detection, not scripted outcomes.** Where the demo shows a conflict or a fault, it's because the underlying simulation state actually produced one — e.g. Closed Loop checks every cycle whether two enabled rApps genuinely want to act on the same cell, rather than playing back a canned example.
- **State that resolves on its own, imperfectly.** Infrastructure objects can spontaneously degrade and transient states settle back to normal after a while even without intervention, closer to how real infrastructure behaves than a demo where nothing changes unless you click something.
- **A fixed, predictable layout footprint.** Scrollable panels are sized consistently so the page doesn't visibly grow or shift as alarms, sessions, or configuration entries accumulate during a live walkthrough.

## Running locally

No build step, no dependencies, no install:

```bash
git clone https://github.com/yoroyarell/smo-demo.git
cd smo-demo
open index.html   # or just double-click it, or drag it into a browser tab
```

## Tech notes

- Vanilla HTML/CSS/JS — no frameworks, no build tooling.
- Fonts: Space Grotesk (display), IBM Plex Sans (body), IBM Plex Mono (data/technical).
- All charts, diagrams, and the fleet heatmap are hand-rolled SVG/Canvas — no charting library dependency.

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

This is an independent, personal project built for demonstration and portfolio purposes. It is not affiliated with, endorsed by, or built using confidential material from any telecom vendor. All product names referenced (O-RAN, 3GPP, etc.) refer to public industry standards, not any specific commercial product.
