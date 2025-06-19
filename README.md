# Intraday Explosiveness Detection in Financial Markets

This project implements a high-frequency analysis framework to detect episodes of explosive behavior in asset prices using the **GSADF methodology** by Boswijk et al. (2024). The focus lies in testing market bubbles, volatility bursts, and regime shifts across diverse asset classes using **recursive Dickey-Fuller tests** and **realized volatility-based devolatization**.

> Developed as part of the *Financial Big Data* project at EPFL (June 2025).

---

## Motivation

Traditional econometric tools often fall short when it comes to identifying explosive price regimes or early signs of bubbles—especially in high-volatility sectors like crypto or oil. This project uses **5-minute intraday data** to identify significant explosive episodes in:
- US Stocks & Indices (e.g., JPM, NFLX, S&P 500)
- European Equities (e.g., ASML, NOVOB)
- Commodities (e.g., Brent, Gold)
- Forex Pairs (e.g., EUR/USD, USD/JPY)
- Cryptocurrencies (e.g., BTC, ETH)

---

## Repository Structure

| File                          | Purpose                                             |
|-------------------------------|-----------------------------------------------------|
| `fetch_intraday_alpaca.ipynb` | Download high-frequency price data from Alpaca     |
| `merge_intraday_dukascopy.ipynb` | Combine and resample Dukascopy pricing data      |
| `clean_intraday.ipynb`        | Clean and preprocess data for testing              |
| `implementation.ipynb`        | Apply explosiveness detection and plot results     |
| `README.md`                   | Project documentation                              |
| `.gitignore`                  | Ignore checkpoints, system files, and raw data     |

The `data/` folder is expected at the project root and must contain the time series to analyze.

---

## Methodology

###  1. Devolatization
Realized volatility is calculated using high-frequency log returns, and used to scale log-price increments into a devolatized form.

###  2. Recursive Dickey-Fuller (RDF) Testing
We apply a **supremum-augmented Dickey-Fuller test** recursively on sub-samples to detect non-stationary (explosive) behavior.

###  3. RVDF Detector & Data Stamping
Explosive periods are date-stamped using a dynamic threshold and the rolling RDF test statistic.

---

## Key Results

- **JPM stock** showed clear explosiveness between May–Dec 2024 (significant at 1%)
- **SPY** and **EU STOXX 50** showed short explosive phases (~1-2 days)
- **Brent Crude** exhibited consistent explosiveness in 2021–2022
- Surprisingly, **BTC/ETH** showed no explosive behavior based on this test
- **USD/JPY** exhibited sustained explosiveness in late 2024

> or detailed charts, test statistics, and economic interpretation, see the Project Report.

---

## How to Run

1. Clone the repo and create a `data/` directory.
2. Place your 5-minute or 1-day asset price CSVs there.
3. Run the following notebooks in order:
   - `clean_intraday.ipynb`
   - `implementation.ipynb`

> You can change which assets to run tests on by editing the `symbols` variable.

## References
1. Boswijk et al. (2024). Testing for Explosive Behavior in Asset Prices Using High-Frequency Data.
2. Tsay, R. (2010). Analysis of Financial Time Series, 3rd Edition, Wiley.

---
## Authors
1. Aidas Žalys
2. Benjamin Steffen
3. Mayur Agrawal


