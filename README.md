# MNQ-channel-strategy
# MNQ 5m Trend & Channel Strategy (60MA / 20MA)

Author: CHIH.H

---

💡 Strategy Overview

This approach is not based on indicator crossovers.  
It is simply a formal description of how I normally read the chart and execute trades.

> **Trade MNQ on the 5-minute chart using 60MA for market bias,  
> 20MA as an entry filter, trendline for direction control,  
> and channel boundaries as profit targets.  
> If the trendline breaks or turns, the trade is closed immediately.

---

🕒 Timeframe & Moving Average Logic

- Operating timeframe: MNQ 5-minute chart
- Market bias: 60MA
  - 5-minute 60MA approximates 20MA on the 15-minute chart  
  - Used only to determine bullish / bearish / neutral conditions
- Entry filter: 20MA
  - A pullback into 20MA, aligned with 60MA direction, may qualify as an entry

> 60MA decides whether to trade;  
> 20MA filters where to trade.

---

🧱 Entry & Exit Rules

📈 Long Setup (Bullish Market)

✔ `60MA sloping upward`  
✔ Price pulls back near `20MA` while staying above the trendline  
✔ A candle resumes upward movement along the trend direction

→ Enter long

📉 Short Setup (Bearish Market)

✔ `60MA sloping downward`  
✔ Price pulls back near `20MA` while staying below the trendline  
✔ A candle resumes downward movement along the trend direction

→ Enter short

---

🎯 Exits: Profit & Risk

- Profit target
  - Long → channel upper boundary
  - Short → channel lower boundary  
  → Only capture one portion of the move; do not force extensions.

- Stop Loss
  - Trendline breaks or visibly reverses
  - Strong close beyond 20MA against the trade  
  → Assume the trend is invalid and exit immediately.

> We trade structure continuation, not reversal prediction.

---

📊 Example Chart

Below is a real example:  
In a bearish channel, shorts are taken at the upper boundary and profits are taken at the lower boundary.  
We avoid trading the “sliding middle area” with low edge.

![MNQ Channel Example](images/mnq_channel_example.jpg)

---

🔧 Pseudocode (Strategy Skeleton)

```python
# MNQ 5-minute strategy
ma60 = SMA(close, 60)   # Market bias (≈ 15m 20MA)
ma20 = SMA(close, 20)   # Entry filter (pullback area)

if slope(ma60) > 0:  # Bullish environment
    if price_near(ma20) and trendline_up():
        enter_long()
        stop_loss  = below_trendline()
        take_profit = channel_upper()

elif slope(ma60) < 0:  # Bearish environment
    if price_near(ma20) and trendline_down():
        enter_short()
        stop_loss  = above_trendline()
        take_profit = channel_lower()

else:
    pass  # Neutral → No trade
