# NBFC Intelligence Dashboard — Session Context

> **Purpose of this file**: Persist full build context so any future Claude session can resume instantly without re-reading the codebase or re-extracting data.

---

## Project Overview

**Goal**: Build a premium, standalone `index.html` dashboard for NBFC (Non-Banking Financial Company) benchmarking — no Streamlit, no server, just open the HTML file in a browser.

**Source repo (data)**: `https://github.com/vibhorjain27/nbfc-dashboard`
- `nbfc_data_cache.py` — financial metrics (Q3FY26 snapshot + 8-quarter time series)
- `nbfc_ai_data.py` — AI initiatives per NBFC
- `shareholding_data.py` — shareholding patterns (optional, add if time permits)

**Destination repo (this one)**: `https://github.com/vibhorjain27/nbfc-intelligence`
- Branch: `claude/review-project-codebase-awUPX`
- Output file: `index.html`

---

## Design Decisions

### Theme
- **Background**: `#0a0e1a` (deep navy)
- **Cards**: `rgba(255,255,255,0.05)` glassmorphism, border `rgba(255,255,255,0.08)`
- **Font**: Inter (Google Fonts)
- **Tab indicator**: bottom-border accent line on active tab

### Per-NBFC Accent Colours
| NBFC | Colour |
|------|--------|
| Bajaj Finance | `#FF6B35` |
| Shriram Finance | `#4A9EFF` |
| Chola Finance | `#34C785` |
| Muthoot Finance | `#FFD700` |
| Aditya Birla Capital | `#B06AE8` |
| Mahindra Finance | `#FF4757` |
| L&T Finance | `#1E90FF` |
| Piramal Finance | `#20E3C4` |
| Poonawalla Fincorp | `#FF8C69` |

---

## Dashboard Tabs

| # | Tab Name | Status |
|---|----------|--------|
| 1 | Snapshot | In build |
| 2 | Peer Comparison | In build |
| 3 | Charts | In build |
| 4 | Time Series | In build |
| 5 | AI Initiatives | In build |
| 6 | Capital Adequacy | In build |

### Tab 1 — Snapshot
- Hero: "NBFC Intelligence | Q3 FY26"
- 9 NBFC cards (3-col grid): name, ticker, segment, AUM, PAT, ROA, ROE, GNPA, NNPA, NIM
- AUM ranking horizontal bar chart (Chart.js)

### Tab 2 — Peer Comparison
- Sortable table: 9 NBFCs × 12 metrics
- Columns: AUM, PAT, NIM, ROA, ROE, GNPA, NNPA, PCR, Cost of Borrowing, D/E, CAR, BVPS
- Red→Green heatmap per column; None = "—"
- Sticky header

### Tab 3 — Charts
- 2×2 grid of Chart.js charts:
  1. Horizontal AUM bar (sorted)
  2. ROA vs ROE scatter (bubble size = AUM)
  3. NIM vs GNPA scatter (labelled)
  4. Cost of Borrowing bar (sorted)

### Tab 4 — Time Series
- Dropdowns: select NBFC + metric
- 8-quarter line chart (Q4FY24–Q3FY26)
- Multi-NBFC compare toggle buttons
- null for missing values (Chart.js spanGaps: false)

### Tab 5 — AI Initiatives
- Filter: by NBFC + by function category
- 3-col card grid, each card: NBFC badge, title, description (3-line clamp + "Read more"), impact box, function pills, source link, date
- 41 total initiatives across 8 NBFCs

### Tab 6 — Capital Adequacy
- Multi-line Chart.js: CAR % for all NBFCs over 8 quarters
- Table below: CAR, T1, T2 per NBFC per quarter

---

## Full Embedded Data

### 9 NBFCs — Q3 FY26 Snapshot

```
Bajaj Finance       | AUM 485,883 Cr | PAT 5,317 | ROA 4.6% | ROE 19.6% | GNPA 1.21% | NNPA 0.47% | NIM N/A    | PCR 61.0% | CoB 7.45% | D/E 4.75 | CAR 21.45% | BVPS ₹170
Shriram Finance     | AUM 291,709 Cr | PAT 2,522 | ROA 3.09% | ROE 16.33% | GNPA 4.54% | NNPA 2.38% | NIM 8.58% | PCR 48.77% | CoB 8.0% | D/E 4.05 | CAR 20.27% | BVPS ₹330
Chola Finance       | AUM 227,770 Cr | PAT 1,288 | ROA 3.2%  | ROE 19.1%  | GNPA 3.36% | NNPA 1.91% | NIM 8.0%  | PCR 43.0%  | CoB 6.7%  | D/E 7.5  | CAR 19.16% | BVPS ₹327
Muthoot Finance     | AUM 164,720 Cr | PAT 2,824 | ROA 7.59% | ROE 32.03% | GNPA 1.58% | NNPA N/A   | NIM 12.77% | PCR N/A   | CoB 8.9%  | D/E 3.40 | CAR N/A    | BVPS ₹859
Aditya Birla Cap    | AUM 148,182 Cr | PAT 772   | ROA 2.25% | ROE 15.2%  | GNPA 1.51% | NNPA 0.84% | NIM 6.12% | PCR 44.3%  | CoB 6.56% | D/E 4.59 | CAR 17.34% | BVPS ₹106
Mahindra Finance    | AUM 128,965 Cr | PAT 810   | ROA 1.9%  | ROE 11.8%  | GNPA 3.80% | NNPA 1.82% | NIM 7.5%  | PCR 53.0%  | CoB 6.0%  | D/E 4.87 | CAR N/A    | BVPS ₹171
L&T Finance         | AUM 114,285 Cr | PAT 760   | ROA 2.37% | ROE 11.38% | GNPA 3.19% | NNPA 0.92% | NIM 8.58% | PCR 72.0%  | CoB 7.25% | D/E 3.78 | CAR 19.10% | BVPS ₹108
Piramal Finance     | AUM  96,690 Cr | PAT 401   | ROA 1.9%  | ROE N/A    | GNPA 2.6%  | NNPA 1.9%  | NIM 6.3%  | PCR 27.9%  | CoB 8.9%  | D/E 2.71 | CAR N/A    | BVPS ₹1,232
Poonawalla Fincorp  | AUM  55,017 Cr | PAT 150   | ROA 1.20% | ROE N/A    | GNPA 1.51% | NNPA 0.80% | NIM 8.62% | PCR 47.75% | CoB 7.65% | D/E 4.25 | CAR 18.17% | BVPS ₹124
```

### 8-Quarter Time Series (Q4FY24 → Q3FY26)

All data available in `/home/user/nbfc-dashboard/nbfc_data_cache.py` under `NBFC_TIMESERIES`.

Quarters: `["Q4FY24","Q1FY25","Q2FY25","Q3FY25","Q4FY25","Q1FY26","Q2FY26","Q3FY26"]`

Metrics available per NBFC (16 each):
`aum_cr, gnpa_pct, nnpa_pct, pcr_pct, pat_cr, nim_pct, roa_pct, roe_pct, cost_of_borrowing_pct, d_e_ratio, car_pct, t1_pct, t2_pct, bvps_inr`

Poonawalla also has: `net_worth_cr` (only in snapshot, not timeseries)

### AI Initiatives — 41 total

| NBFC | Count |
|------|-------|
| Bajaj Finance | 8 |
| Shriram Finance | 5 |
| L&T Finance | 6 |
| Cholamandalam Finance (= Chola Finance) | 5 |
| Aditya Birla Capital | 6 |
| Piramal Finance | 5 |
| Muthoot Finance | 5 |
| Mahindra Finance | 5 |
| Poonawalla Fincorp | 6 |

Function taxonomy (9 categories):
- Credit Underwriting & Risk
- Customer Service & Chatbots
- Collections
- Sales & Marketing
- Digital Lending & Origination
- Document Processing & KYC
- HR & Operations
- Compliance & Governance
- Strategy & Partnerships

---

## Build Status

| Item | Status |
|------|--------|
| `index.html` | **Building (agent running)** |
| Git branch `claude/review-project-codebase-awUPX` | Pending push |
| CONTEXT.md (this file) | ✅ Done |

---

## How to Resume

If tokens run out mid-build:

1. **Check if `index.html` was written**: `ls -lh /home/user/nbfc-intelligence/index.html`
2. **If missing** — re-run the Write agent with the full data above, target `/home/user/nbfc-intelligence/index.html`
3. **If partial** — Read the file, identify what tabs are missing, continue writing
4. **Push command**:
   ```bash
   cd /home/user/nbfc-intelligence
   git checkout -b claude/review-project-codebase-awUPX 2>/dev/null || git checkout claude/review-project-codebase-awUPX
   git add index.html CONTEXT.md
   git commit -m "Add premium standalone HTML NBFC Intelligence dashboard"
   git push -u origin claude/review-project-codebase-awUPX
   ```
5. **Then create PR**: `gh pr create --repo vibhorjain27/nbfc-intelligence --base main --head claude/review-project-codebase-awUPX --title "Premium HTML NBFC Intelligence Dashboard" --body "..."`

---

## Tech Decisions Already Made

- Chart.js 4.4.0 from `https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js`
- No build tools, no npm, no frameworks — pure HTML/CSS/JS
- `spanGaps: false` for time series charts (breaks line at null)
- Chart.js global defaults: white text, dark grid lines
- Heatmap: per-column min/max normalization → green (best) to red (worst)
- Metric display: NIM/ROA/ROE/GNPA/NNPA = 2 decimal places + %; AUM/PAT = ₹ Cr with commas; D/E = 2dp + x; BVPS = ₹ + 2dp

---

*Last updated: March 2026 | Session: claude/review-project-codebase-awUPX*
