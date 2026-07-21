# Statistical Arbitrage Trading Engine

An end-to-end quantitative trading framework designed to identify, backtest, and execute statistical arbitrage strategies across financial markets. The project uses cointegration analysis, mean-reversion modeling, dynamic hedge ratio estimation, and risk management to exploit pricing inefficiencies between correlated assets.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Trading Strategy](#trading-strategy)
- [Tech Stack](#tech-stack)
- [Installation and Setup](#installation-and-setup)
- [Usage](#usage)
- [Results and Metrics](#results-and-metrics)
- [License](#license)

---

## Overview

Statistical arbitrage relies on mathematical models to detect transient relative mispricings between financial instruments. This project implements a fully automated pipeline that:

1. Filters a target asset universe for cointegrated pairs.
2. Models time-varying spread dynamics and optimal hedge ratios.
3. Generates trade signals based on standardized z-score threshold crossings.
4. Simulates execution with realistic market parameters (slippage, transaction costs, borrow rates).
5. Enforces risk controls to handle cointegration breakdown and structural regime shifts.

---

## Key Features

- **Automated Cointegration Screening:** Statistical testing using Augmented Dickey-Fuller (ADF) and Johansen Cointegration tests.
- **Dynamic Hedge Ratio Estimation:** Ordinary Least Squares (OLS) baseline and Kalman Filter for adaptive, real-time hedge ratio adjustments.
- **Signal Generation Engine:** Rolling z-score normalization with configurable entry, exit, and stop-loss boundaries.
- **Vectorized Backtesting:** Robust backtesting module accounting for commission fees, bid-ask spread slippage, and short-selling borrow costs.
- **Risk Management Module:** Continuous delta/market-neutral exposure maintenance and automated stop-loss triggers during structural breaks.

---

## Architecture

The system consists of four primary modules:

1. **Data Module (`/src/data`):** Handles data ingestion, time-zone synchronization, alignment, and missing data imputation.
2. **Analysis Module (`/src/analysis`):** Conducts stationarity, cointegration, and correlation screening across asset pairs.
3. **Strategy Module (`/src/strategy`):** Computes dynamic spreads, z-scores, and entry/exit trading signals.
4. **Execution & Backtest Module (`/src/backtest`):** Simulates portfolio execution, tracks pnl, and evaluates performance metrics.

---

## Trading Strategy

### Pair Selection
Pairs are selected based on pair-wise correlation and confirmed via cointegration tests:
- **Stationarity Check:** Augmented Dickey-Fuller test on individual series.
- **Cointegration Test:** Engle-Granger two-step method and Johansen test on combined series.

### Signal Formulation
- Spread calculation: `Spread = Asset_A - (Hedge_Ratio * Asset_B)`
- Z-Score calculation: `Z = (Spread - Rolling_Mean(Spread)) / Rolling_Std(Spread)`

### Execution Rules
- **Long Spread (Buy A, Sell B):** Z-Score < -2.0
- **Short Spread (Sell A, Buy B):** Z-Score > +2.0
- **Close Position:** |Z-Score| <= 0.5
- **Stop Loss Trigger:** |Z-Score| >= 3.5

---

## Tech Stack

- **Language:** Python 3.10+
- **Data & Computation:** Pandas, NumPy, Statsmodels, SciPy
- **Visualization:** Matplotlib, Seaborn
- **Data Providers:** YFinance / Financial APIs

---

## Installation and Setup

### Prerequisites

Ensure you have Python 3.10 or higher installed.

### Environment Setup

1. Clone the repository:
   ```cmd
   git clone [https://github.com/karim31003/Statistical-Arbitrage.git](https://github.com/karim31003/Statistical-Arbitrage.git)
   cd Statistical-Arbitrage
