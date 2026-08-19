# Qualitas — Quality Intelligence Platform

A futuristic, single-page dashboard for BPO call & email quality audits. Upload your audit tracker (`.xlsx`) and instantly get weekly & monthly leaderboards, parameter-wise coaching insights, and fatal-rate tracking — no backend, no database, no install.

### 🔗 Live site
**[https://raul-2000.github.io/quality-dashboard/](https://raul-2000.github.io/quality-dashboard/)**
**[https://qualitydb.pages.dev/](https://qualitydb.pages.dev/)**

---

## What it does

- **Drag-and-drop upload** of any `.xlsx` quality audit sheet
- **Auto-detects columns** by header text (Advisor name, Audit Date, and all 9 quality parameters), so it adapts even if column order changes
- **Automated scoring engine**, matching standard BPO QA rules — see [Scoring rules](#scoring-rules) below
- **Live filters**: Month and Week (1st–7th, 8th–14th, 15th–21st, 22nd–end), applied instantly across every chart and table
- **Executive KPIs**: Total Audits, Avg Quality Score, Fatal Audits, Fatal Rate, Top Performer, Needs Coaching
- **Charts**: Top 10 performers, weekly quality trend, fatal vs non-fatal split, parameter-wise team average
- **Sortable, searchable leaderboard** with gold/silver/bronze rank badges
- **Parameter-wise heatmap table** per agent, for targeted coaching
- Remembers your last uploaded file in the browser between visits, so you don't have to re-upload every time

## Privacy — read this first

This tool has **no backend and no database**. Your Excel file is read and scored **entirely inside your own browser tab** using JavaScript — nothing is ever uploaded, emailed, or sent to any server, including GitHub. That means:
- It's safe to use with real agent names and customer-related audit data
- Each person who opens the site works with their own uploaded file only
- Closing the tab / clearing browser storage will remove the saved data from that browser

---

## How to use it

1. Open **[the live site](https://raul-2000.github.io/quality-dashboard/)**
2. Drag your `.xlsx` audit file onto the upload box (or click it to browse your files)
3. Wait a second while it parses — it will tell you how many rows it found and from which sheet
4. Use the **Month** and **Week** dropdowns at the top of the dashboard to filter everything at once
5. On the leaderboard table:
   - Click any **column header** to sort by it (click again to reverse)
   - Use the **search box** to jump to a specific advisor
6. To load a different file later, click **"Upload new file"** in the top right

No installation, login, or account is required — it works the same on desktop, laptop, or tablet, in any modern browser (Chrome, Edge, Safari, Firefox).

---

## Excel format needed

The sheet doesn't need to match an exact template — the app scans column **headers** for keywords and figures out which column is which. It works with the tracker exported from this project, or your own raw sheet, as long as it has these columns somewhere:

| What it's looking for | Header keywords it recognizes | Required? |
|---|---|---|
| Advisor / agent name | "Advisor name", "Advisor", "Agent name" | ✅ Required |
| Audit date | "Audit Date" | Used to bucket into Week 1–4 |
| Conversation date | "Conversation Date" | Used as backup if Audit Date is blank |
| Audit month | "Audit Month" | Used as backup for month grouping |
| Communication (10 pts) | "Communication" | Recommended |
| Proper Probing (10 pts) | "Probing" | Recommended |
| Ack / Apology (10 pts) | "Ack" | Recommended |
| Tagging (10 pts) | "Tagging" | Recommended |
| System Navigation (15 pts) | "System Navigation" / "Navigation" | Recommended, can be `Fatal` |
| Ownership / Empathy (15 pts) | "Ownership" / "Empathy" | Recommended, can be `Fatal` |
| Correct & Complete Resolution (15 pts) | "Correct & Complete" / "Resolution" | Recommended, can be `Fatal` |
| Escalation Followed (10 pts) | "Escalation" | Recommended, can be `Fatal` |
| Script Adherence (5 pts) | "Script" | Recommended |

**Notes:**
- Column **order doesn't matter** — only the header text does.
- If your workbook has multiple sheets (e.g. a raw data tab plus dashboard tabs), the app automatically picks the sheet that best matches this column list.
- Each row needs a non-blank advisor name to be counted — blank rows are skipped automatically, so it's safe to leave extra empty rows for future data entry.

## Scoring rules

Every audit is scored out of 100:

- Type a **number** for any parameter to score it normally out of its max points (10, 15, or 5 as shown above).
- Type **`NA`** (or `N/A`) if that behavior didn't apply to the call/email — it's counted as **full marks** for that parameter.
- Type **`Fatal`** on System Navigation, Ownership/Empathy, Correct & Complete Resolution, or Escalation Followed if it was a critical failure — this makes the **entire audit score 0**, and it's flagged as a Fatal audit everywhere in the dashboard (these 4 parameters are the only ones that support a Fatal marking).
- All other parameters (Communication, Probing, Ack/Apology, Tagging, Script Adherence) only support numeric scores or `NA`.

The **Actual Quality Score** shown throughout the dashboard is this per-audit percentage, averaged across every audit that matches your current Month/Week filter.

---

## Tech stack

- Vanilla HTML / CSS / JavaScript — no build step, no framework, no npm install
- [SheetJS](https://sheetjs.com/) — reads `.xlsx` files entirely in-browser
- [Chart.js](https://www.chartjs.org/) — all charts
- Fonts: Space Grotesk, Inter, JetBrains Mono (Google Fonts)

## Running it locally instead of the hosted version

Just download `index.html` and double-click it — it opens in your default browser and works exactly the same, fully offline (except for loading fonts/charts from their CDNs). No server required.

## Deployment (for maintainers)

This repo is served via **GitHub Pages**, configured under `Settings → Pages → Deploy from branch → main → / (root)`. The file that gets served must be named exactly `index.html` in the repo root. To update the live site, upload a new version of `index.html` (same exact filename) and commit — GitHub Pages redeploys automatically within about a minute.
