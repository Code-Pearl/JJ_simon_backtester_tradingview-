# JJSimon Strategy By K - Backtester - BY CODE__PEARL 

> A sophisticated Pine Script trading strategy for backtesting with session-based fair price tracking, breakout detection, and dynamic risk management.
>
!test.png[test curve] 

## 📋 Overview

The **JJSimon Strategy By K - Backtester** is a comprehensive trading strategy implementation for TradingView's Pine Script v6. It combines multiple technical approaches including:

- **Session-based fair price tracking** across multiple trading sessions
- **Break of Structure (BOS) detection** for trend confirmation
- **Displacement candle patterns** (Marubozu & Upper Wick)
- **Dynamic risk management** using ATR-based position sizing
- **Advanced entry filtering** with direction and time-based constraints

## ✨ Key Features

### 🔄 Session Management
- **4 customizable trading sessions** with independent time windows
- Fair price (session open) tracking with visual markers
- Session linking capability (S2 can link to S1 fair price)
- Visual session price lines and labels

### 📊 Signal Generation
- **Displacement candle detection** with two styles:
  - Upper Wick detection
  - Marubozu style (minimal wicks)
- **Swing point identification** (Higher Highs/Lower Lows)
- **Break of Structure (BOS)** confirmation option
- Directional filtering based on fair price proximity

### 📈 Risk Management
- **ATR-based stop loss calculation** with 3-tier system
- **Multiple TP (Take Profit)** relative to stop loss
- **Fair price SL adjustment** (move stop to entry at fair price)
- Minimum TP distance filtering relative to fair price

### 🎨 Visual Features
- **Trade setup visualization** with risk/reward boxes
- BOS trend lines with configurable visibility
- Session fair price markers
- Signal arrows and displacement bar coloring

## 🛠️ Configuration Options

### Session Settings
| Parameter | Description | Default |
|-----------|-------------|---------|
| Session 1 (930) | Pre-market/opening session | 9:30 - 11:00 |
| Session 2 (1400) | Mid-day session | 14:00 - 15:30 |
| Session 3 (2000) | Evening session | Disabled |
| Session 4 (300) | Overnight session | Disabled |
| Link S2 to S1 | Use S1 fair price for S2 | Disabled |

### Signal Settings
| Parameter | Description | Default |
|-----------|-------------|---------|
| Require BOS | Break of Structure required | Enabled |
| Skip First Mins | Min bars before entry allowed | 0 |
| Against-Fair Trades (mins) | Allow counter-trend trades | 15 |
| TP Multiple | TP relative to SL | 1.5× |
| Max Setups | Visible trade setups | 30 |

### Risk Settings (ATR-based SL)
| Condition | SL Ticks |
|-----------|----------|
| ATR < 7.0 | 66 ticks |
| 7.0 ≤ ATR < 20.0 | 100 ticks |
| ATR ≥ 20.0 | 200 ticks |

## 🚀 How It Works

### 1. Session Detection
The strategy monitors multiple time windows and records the opening price (fair price) when each session begins. These prices serve as reference levels for directional bias.

### 2. Displacement Detection
The strategy identifies strong directional candles using:
- **Upper Wick Style**: Bullish candles closing near high or bearish candles closing near low
- **Marubozu Style**: Candles with minimal total wick relative to range

### 3. Break of Structure (BOS)
Higher Highs and Lower Lows are tracked and when broken, BOS lines are drawn. This provides trend confirmation when combined with displacement signals.

### 4. Signal Generation
A trade signal is generated when:
- Displacement candle occurs within an active session
- Direction aligns with fair price (or within allowed against-fair period)
- BOS confirmation (if enabled)
- ATR filter passes (if enabled)
- TP distance from fair price meets minimum threshold (if enabled)

### 5. Risk Management
- Stop loss is set based on ATR-derived tick distance
- Take profit is a multiple of stop loss
- Optional SL adjustment to entry price when fair price is hit
- Position size is determined by equity percentage (default: 100%)

## 📊 Visual Indicators

The strategy provides extensive visual feedback:

- **Green/Red Arrows**: Long/Short trade signals
- **Yellow Lines**: Session fair prices
- **Risk Boxes (Red)**: Stop loss area visualization
- **Reward Boxes (Green)**: Take profit area visualization
- **White Bar Coloring**: Displacement candles
- **BOS Lines**: Trend break indicators

## 🎯 Strategy Logic Flow

```
1. Check active session window
   ↓
2. Record fair price if session opening
   ↓
3. Detect displacement candle
   ↓
4. Verify BOS (if required)
   ↓
5. Check directional validity
   ↓
6. Verify time constraints (skip first mins / against-fair)
   ↓
7. Calculate SL based on ATR
   ↓
8. Calculate TP as multiple of SL
   ↓
9. Generate entry signal
   ↓
10. Execute trade with stop loss and take profit
   ↓
11. Optionally move SL to entry at fair price
```

## 🔧 Technical Requirements

- **Platform**: TradingView
- **Pine Script Version**: v6
- **Timeframe**: Any (optimized for minute-based sessions)
- **Timezone**: America/New_York (configurable)

## 📝 Notes

- The strategy is designed for backtesting purposes
- Sessions are defined in HHMM format (e.g., 930 = 9:30 AM)
- Default tick size is determined by the instrument
- Commission is set to 0% by default (configurable)
- Position sizing: 100% of equity by default

## 🔄 Customization Tips

1. **Adjust Session Times**: Modify start/end times to match market hours
2. **Fine-tune ATR Bands**: Adjust thresholds based on instrument volatility
3. **Modify TP Multiplier**: Increase for trend-following, decrease for scalping
4. **Toggle BOS Requirement**: Try both enabled/disabled for different market conditions
5. **Adjust Max Setups**: Control chart clutter with visible trade history

## 🧪 Backtesting Usage

1. Add to TradingView chart
2. Configure input parameters
3. Set initial capital (default: $100,000)
4. Run strategy tester
5. Analyze performance metrics

---

> **Disclaimer**: This strategy is for educational and backtesting purposes only. Past performance does not guarantee future results. Always conduct thorough testing before using with real capital.
