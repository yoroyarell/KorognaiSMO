# Korognai SMO — Reference Implementation

A single-file, browser-based SMO / Non-RT RIC reference demo — now spanning **RAN, Core and Transport** — with closed-loop rApps/cApps/tApps, FCAPS, slicing, intent-based assurance, conflict resolution, and security by evidence. No backend, no build step, no server required.

Open `index.html` in any modern browser and it runs — from GitHub Pages, any other static host, or straight off your local disk.

---

## What this actually is

One HTML file ships **two linked experiences**:

1. **Korognai SMO (RAN)** — the main site. A RAN-focused SMO / Non-RT RIC reference implementation: architecture, FCAPS, closed-loop rApps, slicing, security, and documentation.
2. **Cross-Domain SMO — concept preview** — reachable from the main site via the pulsing **"Want to see into the future?"** card beside the header. It extends the identical closed-loop philosophy across **Core** (cApps) and **Transport** (tApps) as well as RAN, and opens in a sandboxed `<iframe>` so its tabs, data and scripts never collide with the main app's.

Every number, alarm, topology, and scenario in both is **synthetic** — generated live, in-browser, by JavaScript. Nothing here is live network data, and no vendor's proprietary material is used anywhere in it.

## Quick start

Just open `index.html`. That's it.

- **Hosting it yourself:** works unmodified on GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3, or a plain web server — it's one static file.
- **Custom domain:** fully domain-independent. Point a CNAME at it, change hosts entirely, or open it from `file://` — nothing in the code references a specific URL, so none of it needs reconfiguring when you move it.
- **Deep links:** every tab in both experiences is bookmarkable/shareable via a URL hash, e.g. `yourdomain.com/#intent-based-assurance` or `yourdomain.com/#core-apps`. Hash fragments never touch the server, so this works with zero server-side routing config, on any host.
- **Mobile:** responsive down to phone width — header stacks, tab bar becomes a horizontal swipe strip, and tooltips don't get stuck open on touch devices.

## Korognai SMO (RAN) — what's in it

| Tab | What it shows |
|---|---|
| Overview | Plain-language landing page, executive KPIs, clickable functional clusters |
| RAN Architecture | Interactive RU/DU/CU diagram with the full O1/O2/A1/E2/F1/E1 interface map |
| FCAPS Monitor | Live fault, performance, configuration, trace, and topology/inventory views |
| Closed Loop | Multi-vendor cell ring + 10,000-cell fleet view, driven by 6 real rApps (ESM, ANR, MRO, MLB, COC, PCI) |
| Near-RT RIC | The fast (10ms–1s) E2 control loop and xApps, contrasted against the Non-RT RIC |
| rApp Catalog / Import rApp | Toggleable rApps running genuine reference logic; validate & onboard your own via JSON descriptor |
| Slice Lifecycle | Full NSSI lifecycle (Create → Modify → Monitor & Assure → Decommission) with SLA-vs-intent visualization |
| Conflict Log | Live rApp-vs-rApp conflict detection with 3 resolution strategies |
| Data & Openness | Coverage matrix, disconnect/reconnect resilience simulator, self-serve data routing |
| Cloud & NF Lifecycle | 100-object live infrastructure inventory: Instantiate / Heal / Scale / Upgrade / Terminate |
| Zero-Touch Rollout | 13-step governed commissioning pipeline |
| Security & Trust | Evidence-based security posture + live supply-chain artifact verification |
| Openness Scorecard | Six industry principles, live-computed from actual demo state |
| Documentation | Full glossary, tab-by-tab guide, scenario reasoning, acronym index |
| 50 Design Questions | 224 public-standards-based questions mapped to where this demo answers each one |

## Cross-Domain SMO (concept preview) — what's in it

Same philosophy, extended to all three domains under one control plane, with **RAN & Apps / Core & Apps / Transport & Apps** dropdowns each mirroring the same five-part pattern (Architecture, App Catalog, Import App, Data & Openness, Cloud & NF Lifecycle).

| Tab | What it shows |
|---|---|
| Overview | All 15 functional clusters — RAN, Core, Transport, and every cross-domain tab — each clickable straight to its tab. Plus a note on which terms here are real O-RAN standards and which are this build's own naming (see below). |
| Cross-Domain Topology | Where SMO/Non-RT CIC sits over RAN, transport and core; the interfaces that tie it together |
| Cross-Domain Loop | RAN, Core and Transport closed loops side by side (each with its own ring diagram, KPIs, and trigger buttons), plus a worked cross-domain root-cause-correlation scenario |
| Cross-Domain Conflict | Same-domain conflict resolution for each domain, plus true cross-domain conflict (one domain's fix undermining another's) |
| **Intent-Based Assurance** | State a business outcome in plain language, watch SMO decompose it into per-domain Targets, deploy it, and watch live compliance — a breach genuinely dispatches the responsible app, it doesn't just recolor a badge |
| FCAPS Monitor | Unified Fault/Performance/Configuration feeds across all three domains, equal counts, one color-coded domain chip per row |
| Security & Trust | Same evidence-based posture, now covering Core/Transport artifacts too |
| Openness Scorecard | Same six principles, now scored across rApps *and* cApps *and* tApps together |
| Future & Standards Radar | Honest L0–L5 autonomy self-placement (currently L4) and an 8-item forward-looking radar |
| Documentation | Rebalanced glossary (RAN + Core + Transport + cross-domain/standards + intent-based management), full tab-by-tab guide, scenario reasoning for all three domains *and* the five example intents, design principles, 71-term acronym index |

### A note on naming — what's real, what's this build's own shorthand

- **rApps** are the one genuinely standardized app family here — defined by O-RAN Alliance for the RAN domain.
- **cApps** and **tApps** are this build's own extension of that pattern to Core and Transport — not yet an industry-agreed term the way rApp/xApp are, though they follow the identical detect → decide → act logic deliberately.
- **"Non-RT CIC"** is this build's own relabeling of the real **Non-RT RIC** — done because the same layer now coordinates across all three domains, and "RIC" (*RAN* Intelligent Controller) stops quite fitting once it's not RAN-only. Nothing about the underlying architecture changes.
- **"Non-RT RIC Federation"**, by contrast, *is* a real, current O-RAN WG2 discussion point — it's called out by its real name in this build specifically because it's an actual industry reference, not this build's own naming.

This is stated explicitly in-app (Cross-Domain Overview tab and Documentation glossary), not just here.

## Design principles this demo tries to hold itself to

- **Honesty over polish** — synthetic data is labeled as such throughout; a breach in Intent-Based Assurance genuinely dispatches a fix or honestly logs that it won't self-correct, rather than just recoloring a badge.
- **Public-standards-only sourcing** — grounded in O-RAN Alliance, 3GPP, TM Forum, ETSI, ITU, ONF, GSMA, NIST and CIS material; no vendor-internal or proprietary content.
- **Genuine logic where it matters** — the rApp/cApp/tApp closed loops run real reference algorithms and detect real conflicts live, not staged animations.
- **Practitioner voice** — written the way a working solution architect would explain it to a colleague, not marketing copy.

## Tech notes

- Single HTML file per experience; no framework, no build step, no server.
- The Cross-Domain concept is embedded in the main file as a base64-encoded payload, decoded into an isolated `<iframe>` on demand — this keeps its element IDs and JS globals from colliding with the main RAN app's, since both independently reuse many of the same names.
- URL hash deep-linking works both directions: the parent page can open the iframe straight to a specific tab, and clicking around inside the iframe updates the parent's address bar (`postMessage`, since an iframe can't rewrite its parent's URL directly).
- All charts, diagrams and tables are hand-rolled SVG/HTML/CSS — no charting library dependency.

## Author

Janos (Kornel) Korognai — 21 years in telecom pre-sales and solution architecture (OSS, network management, SMO, Non-RT RIC, rApps, O-RAN) for Tier-1 operators. Independent project. Not affiliated with or endorsed by any vendor.
