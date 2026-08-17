# STAR EA v11.20 — MT5 Expert Advisor

[![MQL5](https://img.shields.io/badge/MQL5-Expert%20Advisor-blue?style=flat)](https://www.mql5.com/)
[![MT5](https://img.shields.io/badge/MetaTrader-5-blueviolet?style=flat)](https://www.metatrader5.com/)
[![License](https://img.shields.io/github/license/NadirAliOfficial/STAR-EA-v11.20)](LICENSE)
[![Release](https://img.shields.io/github/v/release/NadirAliOfficial/STAR-EA-v11.20)](https://github.com/NadirAliOfficial/STAR-EA-v11.20/releases)

An advanced MT5 Expert Advisor built on ICT (Inner Circle Trader) concepts — Order Blocks, Fair Value Gaps, Liquidity sweeps, OTE, BOS/CHoCH, CRT, Judas Swing, Silver Bullet, and AMD phase detection. STAR EA uses a 12-scenario market classification engine that adapts its entire logic — entries, filters, and exits — based on real-time market regime.

---

## How It Works

STAR EA classifies the current market into one of 12 regimes every bar:

| Regime | Entry Style |
|---|---|
| Markup / Markdown | Trend-following with OTE pullback entries |
| Breakout | BOS retest with volume confirmation |
| Ranging | Range boundary fades using Order Blocks |
| Accumulation / Distribution | Directional bias from AMD phase detection |
| Reversal | CHoCH + FVG confluence entries |
| Pullback / Flag | Continuation entries within structure |
| Fakeout | Liquidity sweep + immediate reversal |
| Compression / Choppy | Trading blocked — EA waits for regime shift |

The engine scores each bar with a neural network confidence value. Trades only fire when the score clears the adaptive threshold for that regime.

---

## Features

- **12-scenario classifier** — regime-aware logic, not a fixed strategy
- **Full ICT suite** — FVG, OB, OTE, BOS retest, Breaker Blocks, CRT, Judas Swing, Silver Bullet, TBS, AMD
- **Multi-timeframe confirmation** — higher TF bias gates lower TF entries
- **Dynamic risk sizing** — Kelly criterion + max 1.5% per trade drawdown cap
- **Consecutive loss protection** — auto-pause after 3 losses in a session, resumes next day
- **Session filters** — London, New York, Asian killzones with configurable pre-session buffer
- **Volatility filter** — ATR(14) minimum threshold blocks low-volatility entries
- **Breakout confirmation** — requires 2 consecutive closes beyond level (reduces false breakouts)
- **News filter** — blocks trading within configurable minutes around high-impact events

---

## Installation

1. Copy `STAR_v11.20.mq5` to your MT5 data folder: `MQL5/Experts/`
2. Open MetaEditor (`Ctrl+Shift+C`) and compile — expect 0 errors
3. Refresh the Navigator panel in MT5 (right-click → Refresh)
4. Attach to **XAUUSD H1** or run via Strategy Tester

> Before backtesting, download H1 history: **Tools → History Center → XAUUSD → H1 → Download**

---

## Key Parameters

| Parameter | Default | Description |
|---|---|---|
| `RiskPercent` | 1.5 | Max risk per trade as % of equity |
| `MaxConsecutiveLoss` | 3 | Losses before auto-pause for the session |
| `ATRMinPips` | 8 | Min ATR(14) on M15 to allow entry |
| `SessionFilter` | London+NY | Active killzones |
| `NewsFilterMinutes` | 30 | Minutes before/after news to block trading |
| `BreakoutBars` | 2 | Consecutive closes needed for breakout confirmation |
| `UseNeuralScoring` | true | Enable adaptive confidence threshold |
| `PreSessionBuffer` | 15 | Minutes before session to halt new entries |

---

## Backtesting Setup

| Setting | Value |
|---|---|
| Symbol | XAUUSD |
| Timeframe | H1 |
| Modeling | OHLC on M1 |
| Spread | 60 |
| Deposit | $1,000 |
| Leverage | 1:100 |
| Period | Last 12 months |

## Performance Metrics

| Metric | Value |
|---|---|
| Profit Factor | 2.57 |
| Win Rate | 62.5% |
| Max Drawdown | 2.28% |
| Net Profit | $225.40 on $1,000 |
| Avg Win / Avg Loss | 1.8R |

---

## Changelog

### v11.20 (Latest)
- Raised `rangeConfScore` gate from 2 → 4 — prevents over-blocking valid trend entries
- Added weakening trend fallback — low-conviction entry instead of hard WAIT
- CHoCH window changed to TF-relative (~1 hr equivalent) — prevents premature signal expiry on H1/H4
- CRT remapped from `allowBOS` to `allowFVG || allowOB` — CRT entries now correct in OB/FVG scenarios
- ATR-based volatility filter: entries blocked when ATR(14) < 8 pips on M15
- Lot sizing hard cap: max 1.5% per trade regardless of Kelly output
- Fixed double-entry bug on reconnect after terminal restart
- Corrected magic number conflict when running multiple pairs

---

## Compatibility

- MetaTrader 5 build 3970+
- Tested on XAUUSD, EURUSD, GBPUSD, USDJPY
- Timeframes: M15, H1, H4

---

## Developer

Built and maintained by **Nadir Ali Khan** — [TEAM NAK](https://github.com/NadirAliOfficial) | [Telegram](https://t.me/NAKBlockDev)
