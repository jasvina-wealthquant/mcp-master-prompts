# Example card: short straddle on a 15 minute chart

> A filled Strategy Card for selling an at the money straddle when the combined premium chart turns down. Use it with the [strategy builder master prompt](../strategy-builder-master-prompt.md).

**Idea in plain words.** A straddle is a call and a put at the same strike. Add their prices together and you get one line: the "straddle price". When that line is falling, the market expects less movement and option sellers collect the decay. This card sells the straddle only when its own chart turns down, and exits when it turns back up.

Inspired by a strategy shared by a community member on r/IndiaAlgoTrading.

```text
STRATEGY CARD
Name:                     NIFTY monthly short straddle, 15 min
Idea in one line:         Sell premium when the straddle's own price chart turns down,
                          get out as soon as it turns back up.

MARKET
Instrument(s):            NIFTY monthly options, CE and PE at the same strike
How to pick the contract: Strike = NIFTY 50 spot rounded to nearest 50.
                          Expiry = current monthly expiry from the instruments list.
                          If 7 or fewer calendar days to expiry, use next month instead
                          and exit any position in the current month.
                          While flat, recompute the strike at every candle close.
                          While in a trade, keep tracking the strikes actually held.
Product type:             NRML (overnight allowed)

DATA AND CHART
Timeframe:                15 minute candles aligned to 9:15
Series to analyse:        Straddle price = CE close + PE close, matched per minute,
                          then resampled to 15 min OHLC
Indicators:               50 EMA on the 15 min straddle close
History needed:           10 trading days of 1 minute data for both legs

ENTRY (all must be true)
1. Last closed candle's straddle close is below the 50 EMA
2. A bearish reversal pattern on the latest closed candles:
   bearish engulfing, shooting star, or evening star (define each exactly in STRATEGY.md)
3. No straddle position open (checked with the broker)
4. Enough margin for both legs (broker margin calculator)
Only on a fully closed candle?  yes
Allowed entry window:     9:30 to 15:00
Max entries per day:      2

EXIT (whichever comes first)
Stop loss:                A 15 min candle closes above the 50 EMA
Target:                   Combined premium falls 35% from entry
Time exit:                7 days before expiry (roll to next month)
Trailing rule:            none
Re entry:                 Only on a fresh signal after the exit candle

SIZE AND RISK
Position size:            1 lot (lot size from instruments list)
Max loss per trade:       ₹5,000 on live mark to market, checked every minute
Max loss per day:         ₹10,000, then kill switch
Max open positions:       1 straddle
Margin check before entry: yes

EXECUTION
Order type:               LIMIT near LTP with a small buffer, rounded to 0.05
If not filled:            Modify toward market up to 3 times, 30 seconds apart
If only one leg fills:    Exit the filled leg at once and alert me
Check frequency:          Signals every 15 min close; risk every 1 min

BACKTEST
Period:                   Last 2 years of monthly expiries
Costs to include:         Brokerage, STT, exchange fees, GST, stamp duty,
                          slippage of 1 tick per leg per side
What counts as good:      Profit factor above 1.3, max drawdown under 20% of margin

NOT SURE ABOUT:           Whether to skip entries on event days (RBI policy, budget,
                          monthly expiry week)
```

## What the agent should push back on in Phase 0

A good run of the master prompt will raise questions like these. If yours does not, ask them yourself.

- A short straddle has **unlimited loss** on a big gap. A stop on candle close cannot protect against an overnight gap. Is the ₹5,000 hard stop acceptable with that gap risk, or should it buy cheap far away options as a hedge?
- "Below the 50 EMA" at entry and "closes above the 50 EMA" at exit are very close together. Expect many small stop outs in sideways markets. The backtest should show how often.
- Historical 1 minute option data for strikes that were not at the money at the time may be thin. How should missing minutes be handled?
