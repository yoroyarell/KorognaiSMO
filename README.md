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
| **RAN Architecture** | Interactive RU/DU/CU diagram with the full O1/O2/A1/E2/F1/E1/O-FH interface map |
| **FCAPS Monitor** | Live fault, performance, configuration, trace, and topology/inventory views |
| **Closed Loop** | Multi-vendor cell ring (12-cell sample + a 10,000-cell fleet heatmap) driving real O-RAN SON algorithms — energy saving, mobility robustness, load balancing, outage compensation |
| **Near-RT RIC** | The fast (10ms–1s) control loop over E2, running xApps — deliberately contrasted against the slower Non-RT RIC loop on Closed Loop |
| **rApp Catalog** | Toggleable rApps with real reference logic, each showing which R1 services it consumes |
| **Import rApp** | Validates and onboards a JSON rApp descriptor (O-RAN R1-style schema), running genuine logic for recognized algorithms and an honest monitoring-only stub for anything else |
| **Slice Lifecycle** | Full NSSI lifecycle (create → modify → monitor/assure → decommission) plus SLA-vs-intent visualization |
| **Conflict Log** | Live rApp-rApp conflict detection and resolution (Allow / First-Come-First-Served / Priority-Based Override) |
| **Data & Openness** | Data coverage matrix, a disconnect/reconnect resilience simulator, and self-serve data-routing config |
| **Cloud & NF Lifecycle** | Triggerable network-function lifecycle actions (instantiate/heal/scale/upgrade/terminate) and infrastructure visibility |
| **Zero-Touch Rollout** | A 13-step governed commissioning pipeline (onboard → discover → deploy → commission → validate → audit) |
| **Security & Trust** | Evidence-based security posture (zero-trust, CIS hardening, supply-chain integrity) with a live artifact-verification log |
| **Openness Scorecard** | Six industry-standard evaluation principles, each pre-populated from real state elsewhere in the demo and freely adjustable |

Hover any jargon term throughout the demo (tab names, KPI titles, abbreviations) for a plain-English explanation — the whole thing is built to be equally readable by an engineer and a VP.

## Design choices worth knowing

- **One file, no backend.** Everything — UI, simulation logic, telemetry generation — lives in `index.html`. Nothing depends on a live connection, which matters when you're demoing in a room with unreliable wifi.
- **Honest about synthetic data.** Every screen is clearly marked as simulation. Imported rApps that don't match a recognized algorithm are labeled as monitoring-only stubs rather than silently pretending to run real logic.
- **Grounded in public standards, not vendor lock-in.** Terminology and behavior are drawn from O-RAN Alliance, 3GPP, TM Forum, ETSI, NIST, and CIS public material — no proprietary vendor documentation, confidential material, or trademarked product names are used anywhere in this repo.
- **Scales in the way real tools scale.** The Closed Loop tab includes both a 12-cell interactive sample and a 10,000-cell aggregated heatmap, to make the point that dashboards need aggregation + drill-down at scale, not one dot per cell.

## Running locally

No build step, no dependencies, no install:

```bash
git clone https://github.com/yoroyarell/smo-demo.git
cd smo-demo
open index.html   # or just double-click it, or drag it into a browser tab
```

## Deploying this yourself

The live link above assumes GitHub Pages with a custom domain:

1. Push this repo to GitHub.
2. In **Settings → Pages**, set the source to the `main` branch, root folder.
3. If using a custom domain, add a `CNAME` file (already included in this repo — edit it to your own domain) and point a DNS `CNAME` record at `<your-username>.github.io`.
4. GitHub Pages will serve `index.html` automatically at your domain.

## Tech notes

- Vanilla HTML/CSS/JS — no frameworks, no build tooling.
- Fonts: Space Grotesk (display), IBM Plex Sans (body), IBM Plex Mono (data/technical).
- All charts, diagrams, and the fleet heatmap are hand-rolled SVG/Canvas — no charting library dependency.

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

This is an independent, personal project built for demonstration and portfolio purposes. It is not affiliated with, endorsed by, or built using confidential material from any telecom vendor. All product names referenced (O-RAN, 3GPP, etc.) refer to public industry standards, not any specific commercial product.
