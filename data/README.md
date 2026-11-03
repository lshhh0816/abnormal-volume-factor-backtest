# Data

The original project used licensed CRSP daily stock data accessed through Wharton Research Data Services (WRDS). The raw and processed CSV files are not included in this public repository because access and redistribution are subject to the data provider's licence.

The analysis requires two authorised CSV exports:

```text
data/crsp_simple/raw/crsp_aapl_jpm_xom_2024_2025.csv
data/crsp_simple/raw/crsp_warmup_2023.csv
```

Required CRSP fields:

| CRSP column | Meaning |
|---|---|
| `Ticker` | Stock ticker |
| `DlyCalDt` | Trading date |
| `DlyPrc` | Daily closing price |
| `DlyRet` | Daily stock return |
| `DlyVol` | Daily trading volume |

The late-2023 file is used only as warm-up history for the 66-day NAV calculation. The formal research period is 2024-2025. When the notebook runs, it creates the processed file automatically at:

```text
data/crsp_simple/processed/crsp_aapl_jpm_xom_research.csv
```
