# REPCO Solar Monitoring Center

Single-file solar plant monitoring dashboard. Pure HTML/CSS/JavaScript — no build step, no backend required.

## Live demo
After deploying to GitHub Pages (see below), your dashboard will be available at:
```
[https://<your-github-username>.github.io/<repo-name>/](https://peerapat-charoenkijmongcol.github.io/Solar-Monitoring-Platform/)
```

## Features
- **Monitoring Center** — Overview, Device Management, Site Detail (with site selector, metric picker, per-string monitoring)
- **Alarm** — Filterable alarm table with bulk actions
- **Detailed Analysis** — Multi-parameter time-series chart with CSV/PNG/JPG export
- **Report** — Wizard for PDF / Excel / CSV reports with custom parameters and scheduling
- **CMMS** — Gantt master plan, task list, O&M scope, summary dashboard
- **Plant Configuration** — Plants, Equipment, Data Source, **KPI Mapping** (per-group field mapping with multiplier/offset), **Status Mapping** (per-plant overrides + JSON/CSV import), Alert Thresholds (per-plant + JSON/CSV import)
- **User Management** — Users, Roles, Activity Log

Every chart has CSV + JPG export. All KPI formulas are editable in-page via the Formula Editor and drive the live dashboard calculations.

## Tech stack
- Vanilla HTML / CSS / JavaScript (no framework)
- [Chart.js](https://www.chartjs.org/) (charts)
- [jsPDF](https://github.com/parallax/jsPDF) + jsPDF-AutoTable (PDF report generation)
- [SheetJS / xlsx.js](https://sheetjs.com/) (Excel export)
- Google Fonts: Inter + Montserrat

All libraries are loaded from CDN — open `index.html` directly in any modern browser and it works.

## Local preview
Just open `index.html` in a browser. Or serve via any static server:
```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```
Then visit `http://localhost:8000/`.

## Deploy to GitHub Pages
See the deployment guide in this repository for step-by-step instructions.

## File structure
```
.
├── index.html      # The dashboard (single file, ~270 KB)
└── README.md
```

## License
Proprietary — REPCO internal use.
