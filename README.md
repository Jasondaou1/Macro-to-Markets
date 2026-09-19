# Macro-to-Markets: How Inflation and Interest Rates Shape S&P 500 Performance (2016–2026)

## Project Overview

This project investigates whether, and how strongly, U.S. inflation (CPI) and monetary policy
(the effective federal funds rate) have been associated with S&P 500 index performance and
volatility between July 2016 and mid-2026. It uses three official time series from FRED (Federal
Reserve Economic Data), a fully reproducible Python data pipeline, exploratory and inferential
statistical analysis, and a set of publication-quality visualizations.

The honest headline finding: the direction of the relationship matches financial theory (higher
inflation and faster rate increases are associated with modestly weaker returns and higher
volatility), but the strength of that relationship is weak and not statistically significant at
monthly resolution over this decade — a result the notebook treats as a legitimate finding rather
than something to overclaim past what the data supports.

## Objectives

1. Acquire and validate reliable macro/financial data directly from FRED, with full source
   attribution.
2. Build a single, clean, analysis-ready dataset aligning a daily equity series with two monthly
   macro series.
3. Perform thorough exploratory and statistical analysis of the inflation/rates/market
   relationship.
4. Compare S&P 500 volatility across distinct monetary-policy regimes.
5. Produce a set of clearly labeled, saved visualizations.
6. Translate statistical results into a business-relevant, honestly caveated narrative.

## Dataset Description & Source Attribution

| Series | FRED ID | Publisher | Frequency | Verified Range |
|---|---|---|---|---|
| S&P 500 Index | `SP500` | S&P Dow Jones Indices LLC | Daily (close) | 2016-07-11 to 2026-07-10 |
| Consumer Price Index (All Urban Consumers) | `CPIAUCSL` | U.S. Bureau of Labor Statistics | Monthly | 1947-01-01 to 2026-04-01 |
| Effective Federal Funds Rate | `FEDFUNDS` | Federal Reserve Board of Governors | Monthly | 1954-07-01 to 2026-06-01 |

All three series were retrieved directly from FRED (`fred.stlouisfed.org`), a public,
authoritative redistribution source maintained by the Federal Reserve Bank of St. Louis. Full
reliability, licensing-limitation, and update-frequency notes are documented in Sections 6-7 of
the notebook. See Section 21 (References) for full citations.

## Installation

1. Ensure Python 3.10+ is installed.
2. From this project's root folder, install dependencies:

   ```
   pip install -r requirements.txt
   ```

   (This has been verified to install cleanly into a fresh virtual environment.)

## Execution Instructions

1. Launch Jupyter from this project's root folder:

   ```
   jupyter notebook
   ```

2. Open `Macro_to_Markets_Project.ipynb`.
3. Run all cells top to bottom (*Kernel → Restart & Run All*). By default (`PIN_TO_SNAPSHOT = True`
   in Section 10), the notebook always loads the verified cached snapshots in `data/raw/` rather
   than attempting a live FRED download, which guarantees the exact same 118-row dataset and the
   exact statistics reported throughout this notebook on every run, on any machine. (Live fetching
   can be re-enabled by flipping that flag, but doing so may pull additional months published since
   this snapshot and will change the reported figures — see Section 10 for details.)
4. All figures will regenerate into `figures/` and the cleaned dataset into
   `outputs/processed_data.csv`. A hard assertion runs automatically during this step (Section
   12.7) and will stop the notebook with a clear error if the final dataset shape ever drifts from
   the documented 118 rows × 11 columns — nothing partial or inconsistent can be silently saved.

## Folder Structure

```
.
├── Final_Report.docx                 Full written report (10 pages, 12pt, 1.5 spacing)
├── Macro_to_Markets_Project.ipynb   Main notebook (all analysis, fully executed)
├── README.md                                This file
├── requirements.txt                         Python package dependencies
├── Presentation.pptx                 10-slide presentation deck
├── figures/                                 8 saved, publication-quality charts
│   ├── 01_line_chart_fedfunds_rate.png
│   ├── 02_histogram_monthly_returns.png
│   ├── 03_boxplot_returns_by_regime.png
│   ├── 04_scatter_return_vs_inflation.png
│   ├── 05_correlation_heatmap.png
│   ├── 06_timeseries_sp500_by_regime.png
│   ├── 07_rolling_average_chart.png
│   └── 08_comparative_indexed_trajectories.png
├── data/raw/                                 Created when you run the notebook (Section 10):
│                                              sp500_raw.csv, cpiaucsl_raw.csv, fedfunds_raw.csv
└── outputs/                                   Created when you run the notebook (Section 12.7):
                                                processed_data.csv
```

**`data/raw/` and `outputs/` are not included in this package** — they are regenerated locally the
first time you run *Kernel → Restart & Run All* (see Execution Instructions above). The 8 figures
**are** included already since they were extracted directly from this notebook's own saved output,
so you can review them immediately without running anything.

## The Report (`Final_Report.docx`)

Built directly from this notebook's own analysis (no new numbers, no new claims): 10 pages,
12-point Calibri body text, 1.5 line spacing, with Cover page; Table of Contents/Figures/Tables;
Introduction with Context/Objectives/Importance/Organization; Methodology with AI writing
approach/Data source/Tools used/Approach; Findings and Results with all 8 visualizations and
explanations; Discussion and Insights; Conclusion and Recommendations; References and Appendices.
Verified directly against the document's XML (not just visually) to confirm no stray font sizes or
line-spacing values exist anywhere in the body text, and every Table of Contents/Figures/Tables
page number was checked against the actual rendered PDF rather than estimated. The cover page
lists Jason Daou as author.

## Expected Outputs

Running the notebook end to end (already done for this copy) produces:

- **8 saved chart images** in `figures/`, each titled, labeled, and legended.
- **One cleaned, merged monthly dataset** (`outputs/processed_data.csv`, 118 rows × 11 columns,
  July 2016 – April 2026) used throughout the EDA, statistical analysis, and visualization
  sections.
- **Printed statistical output** inline in the notebook: descriptive statistics, correlation
  matrices, Pearson significance tests, a Welch's t-test comparing volatility regimes, and a
  simple linear regression — all interpreted in the surrounding markdown.

## AI-Assisted Development Disclosure

This project was developed with the assistance of an AI system (Claude, by Anthropic) as a
planning and coding collaborator. Full disclosure of its role and the boundaries of that role —
including the requirement that all outputs be human-reviewed and that final analytical
responsibility rests with me — is documented in Section 8 of the notebook.

## Reproducing This Analysis

1. **Run `Kernel → Restart & Run All`** on the notebook, so that `data/raw/` and
   `outputs/processed_data.csv` are regenerated locally and the built-in integrity assertion
   (Section 12.7) passes.
2. Runtime artifacts (`.ipynb_checkpoints/`, `__pycache__/`, `.venv/`, `venv/`) are excluded via
   `.gitignore` and shouldn't be committed — they're local debugging byproducts, not deliverables.

