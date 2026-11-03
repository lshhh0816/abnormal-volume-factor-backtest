# Abnormal Trading Volume Factor Backtest

This project tests whether unusually high trading volume on positive-return days is followed by stronger short-term stock returns. It uses AAPL, JPM, and XOM as a small cross-sector sample and separates 2024 development results from 2025 time-based validation results.

## Project workflow

1. Load and clean daily CRSP price, return, and volume data.
2. Calculate Normalized Abnormal Volume (NAV) using each stock's previous 66 trading days.
3. Set the abnormal-volume threshold at the 90th percentile of the 2024 NAV distribution.
4. Compare abnormal-volume up days with normal-volume up days over the same subsequent five-day horizon.
5. Backtest a rule that buys at the next trading day's close, holds for five complete returns, and deducts a 0.10% round-trip trading cost.

## Key findings

### Equal-horizon comparison

| Period | Sample | Abnormal observations | Abnormal 5-day return | Normal observations | Normal 5-day return | Difference |
|---|---|---:|---:|---:|---:|---:|
| 2024 | Development | 35 | 0.41% | 378 | 0.46% | -0.05 percentage points |
| 2025 | Validation | 42 | 0.91% | 361 | 0.31% | +0.59 percentage points |

The hypothesis is not consistently supported across both years: the difference is slightly negative in 2024 and positive in 2025.

### Trading backtest

| Period | Sample | Trades | Cumulative return | Annualised Sharpe ratio | Maximum drawdown |
|---|---|---:|---:|---:|---:|
| 2024 | Development | 25 | 5.11% | 1.19 | -3.02% |
| 2025 | Validation | 24 | 7.70% | 0.97 | -6.32% |

The backtest and the equal-horizon comparison answer different questions. Positive strategy returns do not by themselves prove the research hypothesis because the strategy holds cash when no position is active.

## Repository contents

- `notebook.ipynb`: reproducible data pipeline, signal construction, comparison, and backtest. Saved outputs are retained for review.
- `report.pdf`: standalone project report with methodology, pitfalls, efficiency, risk, reflection, and references.
- `data/README.md`: dataset description and access note.

## Data availability

The original analysis used licensed CRSP daily stock data accessed through Wharton Research Data Services (WRDS). Raw and processed CSV files are not distributed in this public repository. See `data/README.md` for the required fields and expected paths.

## Running the notebook

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

Place authorised CRSP exports at the paths described in `data/README.md`, then run `notebook.ipynb` from top to bottom.

## Limitations

- The sample contains only three large-cap US stocks and two research years.
- Stock-day observations are pooled, so stock-specific behaviour may influence the combined result.
- The transaction-cost assumption is simplified.
- The 2025 period is a time-based validation period, not a completely untouched future test.
- The findings show association rather than causality or statistical proof.

