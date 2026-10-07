# Backtesting Lab: Sell in May and Go Away (Python backtest)

Code from the first video on the **Backtesting Lab** YouTube channel: a Python backtest of the "Sell in May and go away" rule on 7 stock markets.

> **Disclaimer:** I am not a SEBI-registered investment adviser or research analyst. This repository is for education only. It is not investment advice, a recommendation, or a forecast. Backtests are hypothetical, ignore many real-world factors, and do not predict future returns. Investing involves risk, including loss of capital.

**Video:** https://youtu.be/VLyYHmNKvKQ

## What the code does

- **Rule tested:** invested November to April, in cash May to October.
- **Markets:** USA (S&P 500), UK (FTSE 100), France (CAC 40), Japan (Nikkei 225), Hong Kong (Hang Seng), China (SSE Composite), India (Nifty 50).
- **Same for every market:** the same rule, the same trading cost and the same two-day execution delay. Only the cash rate differs per country (rough historical approximations).
- **Data:** daily price indices from Yahoo Finance (`yfinance`), up to 31 July 2026. Dividends are not included.

### Main functions

| Function | Purpose |
|---|---|
| `build_positions` | Turns the calendar rule into a 1 (invested) / 0 (cash) signal |
| `net_returns` | Daily return: market return when invested, cash rate when in cash, minus trading cost on each switch |
| `metrics` | Final value, CAGR, max drawdown, simplified Sharpe ratio, number of entries, % time invested |

The position starts earning two days after the signal, to avoid look-ahead bias.

## Run it

```bash
git clone https://github.com/Backtesting-lab/sell-in-may-backtest.git
cd sell-in-may-backtest
python -m venv venv
venv\Scripts\activate        # Windows (macOS/Linux: source venv/bin/activate)
pip install -r requirements.txt
jupyter notebook sell_in_may_global.ipynb
```

Run the notebook from top to bottom. Yahoo Finance data can change over time, so a fresh download may give slightly different numbers than the video.

## Limitations

- Price indices only: no dividends, taxes, currency effects, or broker fees beyond the assumed trading cost.
- Cash rates are approximations, not exact year-by-year figures.
- A backtest describes the past. It does not guarantee anything about the future.

## License

MIT (see `LICENSE`).
