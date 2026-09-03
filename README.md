# Multi-Asset-Portfolio-Performance-Risk-Attribution-Engine

An end-to-end quantitative portfolio analytics system and institutional client reporting dashboard designed for multi-asset strategy evaluation. The engine ingests daily time-series market data, calculates key risk/return metrics, executes Brinson-Fachler performance attribution, models SQL relational schemas, and feeds an interactive Power BI client portal.

---

## Executive Summary & Architecture

Institutional asset managers—such as Goldman Sachs Multi-Asset Solutions (MAS)—require rigorous performance measurement to validate active tactical allocation decisions against benchmark mandates. This pipeline automates the ingestion of time-series asset data, computes risk-adjusted returns, decouples excess returns into allocation effects, and stages analytical datasets for BI reporting.

### Core Workflow:
1. **Data Ingestion & Cleaning:** Fetches 2 years of daily close price data via Python (`yfinance`) for Equities (`SPY`), Fixed Income (`AGG`), and Commodities (`GLD`).
2. **Financial Risk Engineering:** Computes Annualized Return, Volatility, Sharpe Ratio, Tracking Error, and Information Ratio.
3. **Brinson-Fachler Attribution:** Quantifies tactical allocation effects across asset classes against a standard 60/40 benchmark.
4. **Relational Database Staging:** Structures analytical outputs into SQLite relational tables (`fact_daily_returns`, `fact_attribution`, `fact_kpi_metrics`).
5. **Client Portal Dashboard:** Constructs an interactive Power BI dashboard featuring cumulative performance tracking, tactical tilt visual comparisons, and attribution matrices.

---

## Technical Architecture & Tech Stack

* **Language:** Python 3.x
* **Libraries:** `pandas`, `numpy`, `yfinance`, `sqlite3`
* **Database Management:** SQLite3 / SQL
* **Business Intelligence:** Power BI Desktop (DAX, Data Modeling)

---

## Financial Methodology & Analytical Framework

### 1. Risk-Adjusted Metrics
* **Sharpe Ratio:** Measures risk-adjusted excess return over the risk-free rate ($R_f$):
  $$\text{Sharpe Ratio} = \frac{R_p - R_f}{\sigma_p}$$
* **Tracking Error:** Quantifies the annualized standard deviation of excess return relative to the benchmark:
  $$\text{Tracking Error} = \sigma_{(R_p - R_b)} \times \sqrt{252}$$
* **Information Ratio:** Evaluates portfolio manager skill in generating active return relative to active risk:
  $$\text{Information Ratio} = \frac{\text{Annualized } (R_p - R_b)}{\text{Tracking Error}}$$

### 2. Brinson-Fachler Performance Attribution
To explain active outperformance, the **Allocation Effect ($A_i$)** for asset class $i$ is calculated as:
$$A_i = (w_{p,i} - w_{b,i}) \times (R_{b,i} - R_b)$$

*Where:*
* $w_{p,i}$ = Portfolio weight of asset class $i$
* $w_{b,i}$ = Benchmark weight of asset class $i$
* $R_{b,i}$ = Return of asset class $i$ in benchmark
* $R_b$ = Total return of benchmark

---

## Performance Summary

| Metric | Active Portfolio | Benchmark (60/40) | Active Spread / Excess |
| :--- | :--- | :--- | :--- |
| **Annualized Return** | 14.89% | 10.28% | **+4.61%** |
| **Annualized Volatility** | 10.98% | 8.12% | +2.86% |
| **Sharpe Ratio** | 1.36 | 1.27 | **+0.09** |
| **Tracking Error** | 2.00% | - | - |
| **Information Ratio** | 2.41 | - | **High Active Skill** |

---

## Data Model & SQL Schema Design

The engine outputs three relational fact tables designed for star-schema analytics in Power BI:

* **`fact_daily_returns`**: Daily date-stamped price series, daily portfolio returns, and benchmark daily returns.
* **`fact_attribution`**: Asset-level weights (portfolio vs. benchmark), individual asset returns, and calculated Brinson allocation effects.
* **`fact_kpi_metrics`**: Summary table storing annualized metrics, risk parameters, and active performance spreads.

---

## Power BI Client Portal Features

1. **Executive KPI Header:** Displays core risk parameters (Sharpe Ratio, Tracking Error, Information Ratio) side-by-side with benchmark comparisons.
2. **Cumulative Performance Time Series:** Line chart displaying active strategy compound growth vs. benchmark performance over time.
3. **Tactical Allocation Bar Chart:** Visually compares active portfolio tilts against benchmark baseline targets.
4. **Attribution Detail Table:** Comprehensive line-by-line breakdown of allocation contributions per asset class.

---


   git clone [https://github.com/YOUR_USERNAME/multi-asset-portfolio-analytics-engine.git](https://github.com/YOUR_USERNAME/multi-asset-portfolio-analytics-engine.git)
   cd multi-asset-portfolio-analytics-engine
