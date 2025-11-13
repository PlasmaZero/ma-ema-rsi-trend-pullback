# ma-ema-rsi-trend-pullback
TradingView Pine Script® v6 indicator that combines **moving averages** (EMA/SMA) with **RSI** to help identify trend direction, pullback entries, and cleaner exits for day trading and swing trading.

This script is based on the idea of:
- Using **fast & slow MAs** to define the main trend  
- Using **RSI zones and momentum** to time entries on pullbacks or new trend shifts  
- Tracking **position state** so entries and exits are cleaner and easier to read on the chart  

> This is a **technical analysis tool**, not financial advice. Always test on a demo account and use proper risk management. ALWAYS BACKTEST BEFORE USING REAL CAPITAL.

## Features
- Supports **EMA or SMA** for both fast and slow moving averages  
- Configurable **fast/slow MA lengths**  
- RSI with configurable:
  - Overbought level
  - Oversold level
  - Midpoint (for momentum & trend confirmation)
- Three **Entry Modes** AND **Exit Modes**:
  1. **RSI Crossover Only** – strict, fewer but cleaner signals  
  2. **RSI Zone + MA** – signals when RSI + pullback to MA align  
  3. **Multiple Signals** – combines crossovers, pullbacks, new trend, and RSI momentum shift (Safest option for signals (reduces number of fake signals/fake breakouts/breakdowns))
-  **Position tracking** (`flat`, `long`, `short`) so:
  - Exits only occur **after** corresponding entries  
  - Exits have priority over new entries on the same bar
- Visuals:
  - Fast & slow MA plotted on chart  
  - Uptrend/downtrend background shading  
  - Long/short position shading  
  - RSI plotted on chart with OB/OS/Mid lines  
  - Clear **LONG/SHORT/EXIT** markers/signals

# How It Works
### 1. Trend Detection (MAs)
The script uses two moving averages:
- **Fast MA** (default: 21)
- **Slow MA** (default: 50)
- Note: Moving averages are adjustable inputs so if you would like to use something more ideal for daytrading, 9/21 crosses are a good plan!

Main Idea:
- We are in an **Uptrend** if `fastMA > slowMA`
- We are in a **Downtrend** if `fastMA < slowMA`  

The chart background is shaded
- Green for **uptrend**
- Red for **downtrend**

### 2. RSI Logic
RSI is used for:
- Overbought/oversold detection (Generally speaking overbought signals a potential shift to a bearish move and similarly oversold tends to signal a bullish move)
- Momentum shifts around a **midpoint** (default 50)

Key RSI levels:
- `rsiOB` – Overbought (default 65)  
- `rsiOS` – Oversold (default 35)  
- `rsiMid` – Midpoint (default 50)  

Derived conditions:
- `rsiInOversold` – `rsi < rsiOS`  
- `rsiInOverbought` – `rsi > rsiOB`  
- `rsiRising` / `rsiFalling` – compares with previous bar  
- Crossover events used for entries and exits  

### 3. Entry Modes
You can control how strict or aggressive entries are via **Entry Mode**:

#### a) RSI Crossover Only
- Uptrend  + RSI crossing up from oversold  → Long signals
- Downtrend + RSI crossing down from overbought → Short signals
- This mode is the most strict and tends to generate fewer trades

#### b) RSI Zone + MA
Uses a mix of:
- RSI crossings
- Price pulling back between fast & slow MA with RSI near midpoint
- Useful if you want pullback entries in trend

#### c) Multiple Signals (default)
Combines all of the following:
- RSI crossover (from OS/OB)
- Price pullback to MA in trend
- New trend + RSI on correct side of midpoint
- RSI momentum shift across the midpoint in trend
- This is the most flexible/aggressive mode and will typically create more signals.

### 4) Position Tracking With Entries + Exits
Logic:
Exits are checked first on each bar:
- Long Exit: in long & RSI crosses below OB or trend flips down
- Short Exit: in short & RSI crosses above OS or trend flips up

Only after exits are processed do we allow new entries:
- Long Entry: longSignal and not already long
- Short Entry: shortSignal and not already short

Same bar cannot both exit and re-enter the same direction.

# Combine with:
- Support & resistance
- Volume / volatility filters
- Higher timeframe trend bias
- Always backtest and forward-test on paper before trading real money. THIS IS NOT A TOOL WITH GUARANTEED PROFIT. THIS IS NOT FINANCIAL ADVICE.

# How to Use in TradingView
1) Open TradingView and sign in.
2) Go to Pine Editor (bottom of the screen).
3) Copy the indicator code from ma_ema_rsi_trend_pullback.pine.
4) Paste it into the Pine Editor.
5) Click “Add to chart”.
6) Open the Settings for the indicator to:
7) Choose EMA or SMA
8) Adjust MA lengths (e.g. for scalping vs swing)
9) Adjust RSI levels (e.g. 70/30, 80/20, etc.)
10) Pick an Entry Mode that fits your style.

# License & Credits
This Pine Script® code is subject to the terms of the Mozilla Public License 2.0:
https://mozilla.org/MPL/2.0/

Copyright © PlasmaZero