# Observing AI in S&P 500

**Do companies that talk about AI on earnings calls actually become more productive?**

A panel-data study of whether AI mentions in S&P 500 earnings calls translate into measurable workforce productivity gains, measured by Revenue per Employee (RPE).

*DSO 459: Business Analytics with Python · USC Marshall · 2026*
*Team: Carter Sayar, Doga Gucuoglu, Aishna Gupta*

---

## The question

Since ChatGPT launched in November 2022, mentions of "AI" on S&P 500 earnings calls jumped roughly 488% (FactSet, 2025). But is that surge real operational transformation — or just signaling to investors? We tested whether companies mentioning AI more often actually showed higher productivity growth.

## What we built

- **Data pipeline:** Processed 376 earnings-call transcripts through a custom `pdfplumber` pipeline — text extraction, boilerplate removal (cutting to the first "Operator" marker), and scoring against a 13-term GenAI keyword dictionary.
- **Panel dataset:** Merged the transcript signals with WRDS Compustat financials into 250 firm-quarter observations across 19 companies and 4 GICS sectors, spanning 2021 Q4 – 2025 Q4.
- **Nine progressive regression models:** Each designed to rule out a flaw in the last — baseline OLS, company fixed effects, lagged specifications, sector-by-sector models, an interaction model, adoption-stage analysis, and a difference-in-differences design using ChatGPT's launch as a natural experiment.

## Key findings

**1. The obvious answer is wrong.** A naive OLS says AI mentions strongly predict higher productivity (coef +0.186). But that result *reverses* under company fixed effects (−0.034) — the cross-sectional signal was really just sector composition. IT and Financial firms have high RPE by design and also talk about AI more.

**2. There's an upfront cost to going public on AI.** Productivity dips at the quarter of a company's *first* AI mention (−0.059) and then fades — consistent with one-time adoption costs. Early movers who paid that cost before ChatGPT launched saw ~9.5% higher RPE growth afterward.

**3. The effect flips by sector.** Financial firms saw a net positive productivity effect from AI mentions (+0.036); Communication Services saw a net negative (−0.066). Industry implementation capacity, not the AI talk itself, determines the signal.

## Tech stack

`Python` · `pdfplumber` · `pandas` · `numpy` · `statsmodels` (OLS & MixedLM) · `matplotlib` · `yfinance`

## Repo contents

| File | What it is |
|------|-----------|
| `459_Project_Regression.ipynb` | All nine regression models |
| `..._Data_Cleaning.ipynb` | PDF-to-data cleaning pipeline |
| `master_panel.csv` | Final analytical dataset (250 obs) |
| `*.png` | Output charts (DiD, interaction & sector coefficients) |

## A note on data

Raw earnings-call transcripts were accessed through USC's S&P Capital IQ subscription and are **not redistributed here** due to licensing restrictions. This repo contains the derived dataset, code, and outputs only.
