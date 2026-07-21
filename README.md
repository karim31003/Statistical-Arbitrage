# EGX Statistical Arbitrage & Pair Trading Engine

An interactive quantitative research tool and trading engine tailored for screening, analyzing, and visualizing statistical arbitrage opportunities. Built specifically with support for **Egyptian Exchange (EGX)** equities and global tickers, this engine performs log-price OLS regression, Augmented Dickey-Fuller (ADF) stationarity testing, Ornstein-Uhlenbeck half-life estimation, and dynamic z-score signal generation.


## Overview

This project provides an end-to-end framework to analyze pairs trading strategies. It fetches real-time and historical market data via Yahoo Finance, calculates structural stat-arb metrics, and renders a fully reactive IPython control panel. Users can tweak lookback windows, z-score entry thresholds, and distribution parameters on the fly without making network calls or re-running code cells.
