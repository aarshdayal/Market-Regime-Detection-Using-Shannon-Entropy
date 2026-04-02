# Market Regime Detection Using Shannon Entropy

This project implements an **online (look‑ahead‑free) market regime detection** system based on Shannon entropy of returns. It uses a rolling window to compute entropy, applies an online change‑point detection algorithm (PELT) to identify regime shifts, and backtests a simple regime‑switching strategy that allocates between stocks (S&P 500) and bonds (TLT).

## Key Features

- **Rolling Shannon entropy** of daily returns (discretised with expanding bins – no look‑ahead).
- **Online change‑point detection** using the `ruptures` library (PELT algorithm) on a sliding window of entropy values.
- **Regime‑switching strategy**:
  - Low entropy → invest in stocks (S&P 500)
  - High entropy → invest in bonds (iShares 20+ Year Treasury Bond ETF, TLT)
- **No look‑ahead bias** – all decisions use only data available up to that day.
- **Performance metrics** (total return, annualised return, volatility, Sharpe ratio) compared to a 100% stock benchmark.

## Results (2010–2023)

| Metric                     | Strategy (Stocks/Bonds) | Benchmark (100% Stocks) |
|----------------------------|-------------------------|--------------------------|
| Total Return               | 147.50%                 | 421.36%                  |
| Annualized Return          | 6.24%                   | 11.66%                   |
| Annualized Volatility      | 16.30%                  | 17.24%                   |
| Sharpe Ratio (0% risk‑free)| 0.383                   | 0.677                    |

The strategy delivered lower total return and Sharpe ratio than the buy‑and‑hold benchmark, but with slightly lower volatility. This highlights the challenge of timing regime shifts and the need for further optimisation (e.g., tuning the penalty, using a trend filter, or multi‑level allocation).

## Limitations & Future Work
- The PELT penalty was fixed; it can be optimised via grid search.
- The binary allocation (100% stocks / 100% bonds) could be replaced with a smoother allocation (e.g., entropy‑weighted).
- Adding a trend filter (e.g., 200‑day moving average) might improve performance.
- Other entropy measures (permutation entropy, sample entropy) could be tested.
