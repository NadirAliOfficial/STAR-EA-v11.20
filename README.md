# STAR EA v11.20 — MT5 Expert Advisor

An advanced MT5 Expert Advisor built on ICT (Inner Circle Trader) concepts including Order Blocks, Fair Value Gaps, Liquidity, OTE, BOS, CRT, Judas Swing, Silver Bullet, and AMD phase detection.

## Overview

STAR EA implements a 12-scenario market classification engine that adapts entry logic, filtering, and exit behavior based on current market conditions. It supports XAUUSD and major Forex pairs across multiple timeframes.

## Fixes Applied in v11.20

| Fix | Description |
|---|---|
| Scenario Gate (rangeConfScore) | Raised threshold from 2 → 4 — prevents over-blocking valid trend entries in probable range conditions |
| Weakening Trend Fallback | Replaces hard WAIT with low-conviction degraded entry — system remains active in weakening trends |
| CHoCH Window | Changed from fixed 5 bars to TF-relative (~1 hour equivalent) — prevents premature reversal signal expiry on H1/H4 |
| CRT Technique Mapping | Remapped from `allowBOS` to `allowFVG \|\| allowOB` — CRT entries now correctly allowed in OB/FVG scenarios |

## Features

- 12-scenario market classification (Markup, Markdown, Breakout, Ranging, Accumulation, Distribution, Reversal, Pullback, Flag, Fakeout, Compression, Choppy)
- ICT technique suite: FVG, Order Blocks, OTE, BOS Retest, Liquidity, Breaker Blocks, CRT, Judas Swing, Silver Bullet, TBS, AMD
- Multi-timeframe confirmation with regime detection
- Neural network signal scoring with adaptive confidence thresholds
- Dynamic risk management: Kelly sizing, drawdown protection, trailing stops, break-even
- Session-aware filtering: London, New York, Asian killzones
- News filter, correlation filter, spread filter

## Backtesting Setup

- Symbol: XAUUSD
- Timeframe: H1
- Period: Last 12 months
- Modeling: OHLC on M1
- Spread: 60
- Deposit: $1,000 | Leverage 1:100

> **Note:** Before running the backtest, download H1 history in MT5 via Tools → History Center → XAUUSD → H1 → Download to ensure sufficient bar data is available.

## Installation

1. Copy `STAR_v11.20.mq5` to `MT5 Data Folder/MQL5/Experts/`
2. Open MetaEditor (Ctrl+Shift+C) and compile — should show 0 errors
3. In MT5 Navigator panel, right-click → Refresh
4. Attach to XAUUSD H1 chart or run via Strategy Tester

## Baseline Performance (Pre-Fix)

| Metric | Value |
|---|---|
| Profit Factor | 2.57 |
| Win Rate | 62.5% |
| Max Drawdown | 2.28% |
| Net Profit | $225.40 |

## Developer

Built and optimized by **Nadir Ali Khan** — [TEAM NAK](https://github.com/NadirAliOffical)
<!-- updated: 2023-10-18-r01 -->
