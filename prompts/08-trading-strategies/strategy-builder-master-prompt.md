# Strategy builder master prompt

> Turn any trading idea into a tested, logged, risk managed bot. You fill in a one page Strategy Card; the agent restates it, builds it module by module, backtests it, paper trades it, and goes live only when you say so.

**MCPs:** broker market data (Zerodha Kite MCP for quotes and history during design), filesystem, code execution. Live orders go through the bot's own broker API code, never through chat.
**Best for:** anyone who can describe a strategy in plain rules and wants it automated safely
**Typical cost:** a few hours of build time; market data calls only until you go live
**Works with:** Claude Code, or any agent that can write files and run Python

> ⚠️ Automated trading can lose money fast, including more than your margin on short options. This prompt defaults to simulation. Read [SEBI and safety notes](#sebi-and-safety-notes) before going live.

## How to use it

1. Copy the **Strategy Card** below and fill it in. Use plain words. Write "not sure" where you are not sure; the agent will ask.
2. Paste the card, then the **Master prompt**, into Claude Code in an empty project folder.
3. Work through the phases. The agent stops at every gate and waits for you.

Two filled cards to learn from: [short straddle on a 15 minute chart](examples/short-straddle-ema.md) and [point and figure breakout for swing trades](examples/point-and-figure-breakout.md).

## The Strategy Card

```text
STRATEGY CARD
Name:                     {{a short name}}
Idea in one line:         {{why should this make money?}}

MARKET
Instrument(s):            {{e.g. NIFTY monthly ATM options / Nifty 200 stocks / BANKNIFTY futures}}
How to pick the contract: {{e.g. strike = spot rounded to nearest 50; expiry from the instruments list}}
Product type:             {{intraday (MIS) / overnight (NRML or CNC)}}

DATA AND CHART
Timeframe:                {{e.g. 15 minute candles / daily / point and figure 1% box, 3 box reversal}}
Series to analyse:        {{e.g. the instrument itself / CE + PE combined / ratio to index}}
Indicators:               {{e.g. 50 EMA on close; ATR 14; none}}
History needed:           {{e.g. 10 trading days of 1 minute data}}

ENTRY (all must be true)
1. {{condition}}
2. {{condition}}
Only on a fully closed candle?  {{yes / no}}
Allowed entry window:     {{e.g. 9:30 to 15:00}}
Max entries per day:      {{n}}

EXIT (whichever comes first)
Stop loss:                {{rule}}
Target:                   {{rule}}
Time exit:                {{e.g. square off at 15:15 / 7 days before expiry}}
Trailing rule:            {{rule or none}}
Re entry:                 {{when is a new trade allowed after an exit?}}

SIZE AND RISK
Position size:            {{e.g. 1 lot / 2% of capital / fixed rupees}}
Max loss per trade:       {{₹}}
Max loss per day:         {{₹}}
Max open positions:       {{n}}
Margin check before entry: {{yes}}

EXECUTION
Order type:               {{LIMIT with buffer / MARKET}}
If not filled:            {{e.g. modify toward market up to 3 times, 30 seconds apart}}
If only one leg fills:    {{e.g. exit the filled leg and alert me}}
Check frequency:          {{e.g. signals every 15 min close; risk every 1 min}}

BACKTEST
Period:                   {{e.g. last 2 years}}
Costs to include:         {{brokerage, STT, exchange fees, GST, stamp duty, slippage per side}}
What counts as good:      {{e.g. profit factor above 1.3, max drawdown under 15%}}

NOT SURE ABOUT:           {{list anything you have not decided}}
```

## The master prompt

```text
ROLE
You are my trading systems engineer. You turn my Strategy Card into a Python
trading system for my broker ({{broker, e.g. Zerodha Kite Connect}}). You follow the
card exactly. You never add, drop or soften a rule without asking me.

GROUND RULES (apply in every phase)
- Simulation is the default. No real order is ever placed until I type the exact
  words GO LIVE, and even then you confirm the final config with me once first.
- Never place, modify or cancel orders through chat tools or MCP order functions.
  Real orders only ever come from the tested bot code in live mode.
- Read API keys and the daily access token from a .env file. Never hard code, print,
  log or commit credentials. Add .env to .gitignore before the first commit.
- Every fact about a contract (expiry date, lot size, tick size, trading symbol)
  comes from the broker's instruments list, never from memory.
- Market hours, holidays and expiry dates come from the exchange or broker data.
- Signals are evaluated only on fully closed candles. No look ahead, anywhere,
  including in the backtest.
- The broker is the source of truth for positions and orders. Reconcile after every
  order and on every restart.

PHASE 0: UNDERSTAND (no code)
1. Restate my Strategy Card in your own plain words.
2. List every rule that is ambiguous and the two or more ways it could be read.
   Example: "close below the EMA" could mean candle close or the whole candle.
3. List every assumption you would make, and every missing piece (sizing, costs,
   holidays, partial fills, gaps at open, what happens at expiry).
4. Suggest up to 3 risks or failure modes this strategy has that the card ignores.
   Do not change the strategy. Just tell me.
GATE 0: wait for my answers. Then write the final rules to STRATEGY.md and get my OK.

PHASE 1: DATA AND CHART
Build in small modules with tests, in this order:
- config.py    every tunable number from the card, plus DRY_RUN=true
- auth.py      daily login helper that writes the access token to .env
- instruments.py  loads the instruments list, picks contracts per the card
- data.py      historical and live data; builds the series the card names;
               resamples to the card's timeframe aligned to market open
- indicators.py   the card's indicators, with unit tests on known values
- chart.py     saves a chart image per evaluation with indicators and trade markers
Use the market data MCP (read only) to sanity check prices while you build.
GATE 1: show me a chart of the last few sessions with indicators and the signals your
code would have fired. I confirm the signals match what I see by eye.

PHASE 2: SIGNALS AND RISK
- signals.py   entry and exit rules exactly as in STRATEGY.md, each as a named,
               unit tested function. Each decision returns a reason string.
- risk.py      sizing, per trade max loss, per day max loss, max positions, margin
               check using the broker's margin calculator, kill switch (a file named
               STOP in the folder, or the daily loss limit hit, squares off everything
               and halts)
GATE 2: show the test results.

PHASE 3: BACKTEST
- backtest.py  replays history candle by candle through the same signals.py and
               risk.py the live bot will use. Applies all costs in the card, plus
               slippage. No future data at any step.
- Report: number of trades, win rate, average win and loss, profit factor, max
  drawdown, longest losing streak, results by month and by market condition
  (trending up, trending down, sideways, high and low volatility).
- Split the period: build on the first 70 percent, report the last 30 percent
  separately. If the two disagree badly, say so plainly.
- Warn me about any sign of overfitting or too few trades to judge.
GATE 3: we review together. I may change the card. If I do, update STRATEGY.md
and rerun.

PHASE 4: PAPER TRADING (DRY_RUN=true)
- execution.py  order placement, modification, fill checks, partial and single leg
                fill handling, all exactly as the card says. In dry run, simulate
                fills at LTP plus the slippage assumption and log them.
- runner.py     the scheduler: evaluate signals on each candle close, check risk at
                the card's frequency, write state.json, reconcile on restart.
- Logs: signals.csv (every evaluation with inputs, decision and reason) and
  trades.csv (every entry and exit with prices, quantity, costs, P&L, exit reason).
- End of day: a short summary of trades, P&L, rules triggered, and errors.
Run it for at least {{n}} sessions. Compare paper results with what the backtest
would have done on the same days and explain any gap.
GATE 4: I decide whether to go live.

PHASE 5: LIVE (only after I type GO LIVE)
- Show me the full live config once: size, limits, account, static IP in use.
- Start with the smallest size the card allows.
- Keep every dry run safeguard on. Alert me on every order, fill, error and exit.
- If anything unexpected happens (rejected order, position mismatch, stale data,
  lost connection), square off per the card, halt, and tell me. Do not improvise.

COMPLIANCE
- Keep the order rate far below 10 orders per second. Throttle in code.
- Orders must go out from the static IP registered with my broker.
- Add a header comment in runner.py stating the strategy is self built for my
  own account.

STYLE
Small modules, plain names, type hints, docstrings that explain why. After each
module: show the tests, wait for my OK, then move on.
```

## Why it works

- **The card separates thinking from building.** Most bot failures come from rules that were never fully decided. Phase 0 forces every gap into the open before code exists.
- **One signals module serves the backtest, paper trading and live.** If the backtest uses different code from the live bot, its results mean nothing.
- **Gates sit where mistakes are expensive.** Wrong signals are caught on a chart at Gate 1. Wrong strategy is caught at Gate 3. Real money is only at risk after Gate 4 and the GO LIVE words.
- **Chat cannot trade.** Separating MCP research from bot execution means a stray instruction in a conversation can never place an order.

## SEBI and safety notes

Accurate as of October 2026 (check the latest exchange circulars yourself):

- Retail traders can run a self built algo through their broker's API without registering it with the exchange, as long as it stays **below 10 orders per second**. Above that, the strategy must be registered through the broker.
- API orders must come from a **static IP registered with your broker**.
- Selling options carries large and sometimes unlimited risk. Paper trade first, start with one lot, and always have a hard daily loss limit and a kill switch.

This prompt is a starting point for building your own tools. It is not investment advice and not a recommendation of any strategy.

## Variations

- **Alerts only:** remove Phase 5 and have execution.py send you an alert (Telegram, email) instead of placing orders. You trade by hand.
- **Research only:** stop after Phase 3 to test ideas without ever wiring up orders.
- **Many strategies:** keep one folder per Strategy Card and share data.py and execution.py between them.
