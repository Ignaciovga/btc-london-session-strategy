# BTC London Session Strategy

Multi-timeframe backtesting engine for a BTC/USDT intraday strategy based on Tokyo range dynamics and London session liquidity behavior.

---

## Overview

This project implements a quantitative trading strategy using:

* **H1 data** → defines Tokyo session range and daily validation
* **M15 data** → executes trades during the London session
* **1-minute data (on demand)** → resolves ambiguous TP/SL events intrabar
* **Dynamic position sizing** → adapts risk based on volatility conditions

The goal is to model a structured intraday setup and evaluate its performance across multiple years of historical data.

---

## Strategy Logic

1. Define the **Tokyo session range**
2. Validate the trading day using a **specific H1 candle**
3. Monitor price during London session for entry conditions
4. Execute trades based on breakout logic
5. Apply:

   * Stop Loss
   * Take Profit
6. If both TP and SL are touched in the same candle:

   * Resolve using **1-minute Binance data**
7. Track performance and export results

---

## Project Structure

```
.
├── backtest.py          # Main backtesting engine
├── download_data.py     # Script to download historical data (optional)
├── requirements.txt
├── README.md
└── csv/
    ├── BTC_USDT_1h.csv
    └── BTC_USDT_15m.csv
```

---

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## How to Run

The project is designed to run directly using the included CSV files:

```bash
python backtest.py
```

This will:

* run the full backtest
* print a performance summary
* generate an Excel report (`backtest_report.xlsx`)

---

## Data Usage

### Default (Recommended)

The repository already includes the required datasets:

* `BTC_USDT_1h.csv`
* `BTC_USDT_15m.csv`

👉 This is the intended way to run the project.

---

### Optional: Download Data Manually

If you prefer to rebuild the dataset yourself, you can use:

```bash
python download_data.py
```

This will download historical Binance data and regenerate the CSV files.

---

### Intrabar Data (1-minute)

For certain edge cases (when both TP and SL are touched within the same candle), the backtest:

* automatically downloads **1-minute Binance data**
* stores it locally in `data_1m/`
* reuses it for future runs

No manual setup is required for this.

---

## Features

* Multi-timeframe backtesting (H1 + M15 + 1m)
* Dynamic position sizing
* Intrabar execution logic
* Realistic TP/SL resolution
* Full performance analytics:

  * PnL
  * Win rate
  * Drawdown
  * Expectancy
* Excel export with detailed breakdown

---

## Notes

* This project is intended for **research and educational purposes only**
* It does **not** constitute financial advice
* Results depend on data quality and assumptions made in execution logic

---

## Author

Developed as a personal quantitative research project focused on intraday BTC behavior and session-based market dynamics.
