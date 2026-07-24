# Tanni's Quality Dashboards

Two browser-based dashboards for exploring hospital core measure fallouts — where charts fail a quality measure, and why.

**Live site:** https://tannimon.github.io/quality-dashboards/

> ⚠️ **All data in this repository is fictional.** Physician names, site names, compliance rates, and financial figures are invented for demonstration purposes and do not represent any real provider, facility, or patient.

---

## The dashboards

### Fallout Dashboard
A system-wide view of quality performance across sites, measures, and the patient journey. Explore where fallouts occur, what's driving them, and whether performance is improving over time. Drill down by physician to separate provider-specific issues from nursing, process, and system opportunities.

Sample data: 6 sites · 5 measure sets (SEP-1, STK, HBIPS, VTE, IMM-2) · 16 physicians · 1,400 charts

**Accepts your own data.** Upload an `.xlsx` or `.csv` and the dashboard re-renders against it. A blank template is downloadable in-app.

### Physician Accountability Dashboard
A physician-focused view of SEP-1 performance over six months. Track compliance trends, identify recurring fallout patterns, measure the impact of education, and quickly see which providers or cases need leadership attention.

Sample data: SEP-1 · 25 physicians · 214 cases

---

## Privacy

**Uploaded data never leaves your browser.** There is no backend, no server, no analytics on uploaded content, and no network request carrying your file anywhere. Parsing happens entirely client-side via SheetJS. Close the tab and the data is gone.

This matters because quality abstraction files frequently contain PHI. You can open the Fallout Dashboard, upload a real extract, read the charts, and close the tab without anything being transmitted or stored.

That said: this is a demonstration tool published on a public URL. **Follow your own organization's policy** before putting real patient or provider data into any browser tool, including this one.

---

## Upload format (Fallout Dashboard)

One row per chart reviewed. Column headers are matched loosely — `Site`, `site`, `Facility`, and `Hospital` all resolve to the same field.

**Required:**

| Column | Notes |
|---|---|
| `site` | Facility name |
| `measure` | e.g. SEP-1, STK, HBIPS, VTE, IMM-2 |
| `discharge` | Discharge date |
| `status` | Pass / Fallout — also accepts `met`/`not met`, `yes`/`no`, `passed`/`failed` |

**Optional, but each one unlocks more of the dashboard:**

| Column | Enables |
|---|---|
| `reason` | Top Reasons tab, Pareto chart |
| `phase` | Patient-journey funnel — Assessment, Diagnostics, Treatment, Discharge, Follow-up |
| `physician` | By Physician tab |
| `attribution` | Physician / Nursing / System / Mixed — accepts `RN`, `MD`, `provider`, `lab`, `pharmacy`, `shared`, etc. |
| `educationEvent`, `educationDate` | Education-effectiveness panel |
| `crn`, `har` | Case identifiers in the All Cases table |
| `department` | Department grouping |

Rows missing a required field are skipped, and the dashboard reports how many and why.

### Why `attribution` matters

It's the difference between a defensible dashboard and an unfair one. In the sample data, **90% of SEP-1 fallouts are nursing-attributed** — lactate draws, repeat lactate timing, blood cultures before antibiotics. Physicians own STK and VTE failures (NIHSS documentation, statin at discharge, VTE prophylaxis orders), not most SEP-1 ones.

Without this field, a physician scorecard built on SEP-1 blames providers for process failures they didn't cause. With it, each fallout routes to the role that can actually fix it.

---

## Running locally

No build step, no dependencies to install. Clone and open `index.html` in a browser.

```bash
git clone https://github.com/tannimon/quality-dashboards.git
cd quality-dashboards
```

Each dashboard is a single self-contained HTML file. Loaded from a CDN at runtime: SheetJS (spreadsheet parsing), Phosphor Icons, and Google Fonts (DM Sans, DM Mono).

---

## Files

```
index.html                     Landing page
fallout-dashboard.html         System-wide view
physician-accountability.html  SEP-1 physician view
sawyer.jpg                     Chief Morale Officer
```

---

## Built by

Tanni — clinical quality abstractor, vibe code hobbyist, and web design enthusiast. She loves her dog, Sawyer.

Quality-assured by Sawyer, who has reviewed these metrics and has no notes.
