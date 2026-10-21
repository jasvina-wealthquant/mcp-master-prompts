# Example card: point and figure breakout for swing trades

> A filled Strategy Card for buying stocks that break out on a point and figure chart. Use it with the [strategy builder master prompt](../strategy-builder-master-prompt.md).

**Idea in plain words.** A point and figure chart ignores time and small wiggles. It only draws a new mark when price moves by a set amount (the "box"). A column of X's means price is rising; a column of O's means it is falling. A new column starts only after a reversal of several boxes. When a column of X's rises above the top of the last X column, that is a breakout: buyers have pushed past where they gave up last time.

```text
STRATEGY CARD
Name:                     Point and figure double top breakout, daily
Idea in one line:         Buy liquid stocks when they clear their last rally high
                          on a noise filtered chart, and let winners run.

MARKET
Instrument(s):            Nifty 200 stocks (constituents fetched fresh each month)
How to pick the contract: Cash equity, no derivatives
Product type:             CNC (delivery)

DATA AND CHART
Timeframe:                Point and figure from daily closes
Series to analyse:        The stock's daily close
Indicators:               Box size = 1% of price; reversal = 3 boxes;
                          also the Nifty 50 point and figure chart with the same settings
History needed:           2 years of daily candles

ENTRY (all must be true)
1. Double top breakout: the current X column rises one box above the top of
   the previous X column
2. The stock is in a rising pattern: its last X column top is higher than the
   one before it
3. The Nifty 50 chart is in an X column (market not falling)
4. Average daily traded value over 20 days is above ₹20 crore
Only on a fully closed candle?  yes (evaluate after 15:30 on daily close)
Allowed entry window:     Next morning, 9:20 to 10:00
Max entries per day:      3

EXIT (whichever comes first)
Stop loss:                A 3 box reversal into a new O column that falls below the
                          bottom of the previous O column (double bottom breakdown)
Target:                   none, ride the trend
Time exit:                none
Trailing rule:            Raise the stop to the bottom of each new O column as the
                          trend continues
Re entry:                 Allowed on a new breakout after exit

SIZE AND RISK
Position size:            Risk 1% of capital per trade (distance from entry to stop)
Max loss per trade:       1% of capital
Max loss per day:         3% of capital, then halt new entries for the day
Max open positions:       10
Margin check before entry: yes (cash available)

EXECUTION
Order type:               LIMIT at previous close plus 0.3%
If not filled:            Cancel at 10:00, try again only on the next signal
If only one leg fills:    not applicable
Check frequency:          Signals once a day after close; stop check once a day

BACKTEST
Period:                   2018 to today, so it includes the 2020 crash
Costs to include:         Brokerage, STT, exchange fees, GST, stamp duty, 0.1% slippage
What counts as good:      Beats a buy and hold Nifty 200 index fund after costs,
                          with max drawdown under 25%

NOT SURE ABOUT:           Should box size be a fixed 1%, or scaled by each stock's
                          own volatility (average true range)?
```

## What the agent should push back on in Phase 0

- **Survivorship bias.** Today's Nifty 200 list leaves out stocks that were dropped after doing badly. The backtest needs the index membership as it was on each date.
- **Daily closes vs highs and lows.** Point and figure can be built from closes only or from the day's high and low. The two give different charts and signals. Pick one.
- **Gap risk on exits.** A stop checked once a day can be hit far below the level on a gap down. The backtest should fill exits at the next open, not at the stop level.
