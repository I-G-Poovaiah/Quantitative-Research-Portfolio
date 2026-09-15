# Quantitative Systematic Trading Architecture

## Overview
This repository contains the performance analytics and architectural documentation for a proprietary multi-asset trading engine. The core execution logic is built in C# (NinjaTrader 8), utilizing quantitative regime-switching models and statistical variance bands to trade highly liquid U.S. index futures (MES, MNQ). 

Due to IP protection, raw execution source code is kept private. This repository showcases the mathematical architecture, risk-management protocols, and Python-based performance tearsheets (Pandas/Matplotlib) used to validate the models.

## Core Strategy Engines

* **Regime-Based Strategy Engine:** Utilizes a probabilistic regime detection model (approximating a Hidden Markov Model) to classify market states into Trend, Range, Liquidity Sweep, or Volatility Expansion. 
* **Statistical Mean Reversion:** Fades extreme moves during calm/range regimes by identifying when price deviates >1 standard deviation from a rolling mean.
* **Order Flow Vanguard:** Integrates Volume Weighted Average Price (VWAP) alignment and Cumulative Delta divergences to identify institutional absorption and liquidity sweeps.

## Risk Management Architecture
The system employs strict, institutional-grade risk parameters:
* **Dynamic Position Sizing:** Volatility-adjusted position sizing using fractional Kelly criterion formulas to maximize capital growth while capping ruin probability.
* **Portfolio Risk Budgeting:** Hard-coded daily loss limits and maximum trailing drawdowns enforced at the portfolio level.
* **Microstructure Invalidation:** Trailing stops tied to ATR expansion and structural market breaks, rather than arbitrary tick counts.

## Analytics Pipeline
The included Python notebooks ingest raw execution logs (CSV) to calculate institutional metrics:
* Sharpe & Sortino Ratios
* Maximum Peak-to-Trough Drawdown
* Expectancy and Profit Factors

---

## Verified Performance Analytics (Out-of-Sample)

### High-Beta Nasdaq Volatility Engine

**Architecture:** Robust Trend-Pullback Model (SMA / ADX Regime Filter)  
**Instrument:** Micro E-mini Nasdaq-100 (MNQ) — 3-Minute Timeframe  
**Validation:** Rolling Walk-Forward Optimization (30-day train / 15-day out-of-sample test)

| Metric | Out-of-Sample Result |
| :--- | :--- |
| **Total Stitched PnL** | **$3,415.00** |
| **Profit Factor** | **1.19** |
| **Estimated Sharpe Ratio** | **1.55** |
| **Trade Expectancy (Avg Trade)** | **$11.98** |
| **Win Rate** | **28.07%** |
| **Max Peak-to-Trough Drawdown** | **-$2,800.70** |
| **Total Out-of-Sample Executions** | **285 trades** |

![MNQ Volatility Engine OOS](assets/mnq_volatility(robust)_oos.png)
