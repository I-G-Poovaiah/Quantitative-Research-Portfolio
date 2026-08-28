# Quantitative Systematic Trading Architecture

## Overview
This repository contains the performance analytics and architectural documentation for a proprietary multi-asset trading engine. The core execution logic is built in C# (NinjaTrader 8), utilizing quantitative regime-switching models and statistical variance bands to trade highly liquid U.S. index futures (MES, MNQ). 

Due to IP protection, raw execution source code is kept private. This repository showcases the mathematical architecture, risk-management protocols, and Python-based performance tearsheets (Pandas/Matplotlib) used to validate the models.

## Core Strategy Engines

* **Regime-Based Strategy Engine:** Utilizes a probabilistic regime detection model (approximating a Hidden Markov Model) to classify market states into Trend, Range, Liquidity Sweep, or Volatility Expansion[cite: 17]. 
* **Statistical Mean Reversion:** Fades extreme moves during calm/range regimes by identifying when price deviates >1 standard deviation from a rolling mean[cite: 2].
* **Order Flow Vanguard:** Integrates Volume Weighted Average Price (VWAP) alignment and Cumulative Delta divergences to identify institutional absorption and liquidity sweeps[cite: 13].

## Risk Management Architecture
The system employs strict, institutional-grade risk parameters:
* **Dynamic Position Sizing:** Volatility-adjusted position sizing using fractional Kelly criterion formulas to maximize capital growth while capping ruin probability[cite: 2].
* **Portfolio Risk Budgeting:** Hard-coded daily loss limits and maximum trailing drawdowns enforced at the portfolio level[cite: 17].
* **Microstructure Invalidation:** Trailing stops tied to ATR expansion and structural market breaks, rather than arbitrary tick counts[cite: 14].

## Analytics Pipeline
The included Python notebooks ingest raw execution logs (CSV) to calculate institutional metrics:
* Sharpe & Sortino Ratios
* Maximum Peak-to-Trough Drawdown
* Expectancy and Profit Factors
