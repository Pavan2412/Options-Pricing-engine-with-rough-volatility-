# Options-Pricing-engine-with-rough-volatility-
# Volatility-Aware Options Pricing Engine

This repository contains an advanced derivatives pricing pipeline that mirrors a real-world Global Markets workflow. It bridges the gap between sell-side quantitative research and the trading desk by treating volatility forecasting as a first-class research problem, rather than plugging a single static volatility number into pricing models.

The engine generates dynamic volatility forecasts and feeds them directly as the `sigma` input into Black-Scholes, Binomial Tree, and Monte Carlo pricing models to capture implied volatility mispricing under stressed markets.

## 📊 Assets Analyzed
*   **Forecasting Module:** NIFTY 50 (`^NSEI`), S&P 500 (`^GSPC`), and Bitcoin (`BTC-USD`).
*   **Pricing Module:** AAPL (or any liquid single-name equity).

## 🚀 Project Pipeline & Architecture

### Part A: Volatility Forecasting Research
*   **Realized Volatility:** Calculates annualized realized volatility using the Garman-Klass range-based estimator.
*   **Hurst Exponent Estimation:** Estimates roughness (anti-persistence) using the Gatheral-Jaisson-Rosenbaum moment-based scaling law.
*   **Rough Volatility Modeling:** Sets up a fractional Ornstein-Uhlenbeck (fOU) approximation via a fractionally-differenced AR model.
*   **Benchmarking:** Benchmarks against GARCH(1,1), EGARCH(1,1), and HAR-RV.
*   **Validation:** Rolling out-of-sample evaluation with Diebold-Mariano significance tests and crisis-period performance analysis.

### Part B: Options Pricing Engine
*   **Pricing Models:** European option pricing via Black-Scholes (closed-form), Binomial Tree (CRR), and Monte Carlo simulations (GBM).
*   **Greeks & Implied Vol:** Computes real-time Greeks and reverse-engineers implied volatility using Brentq and Newton-Raphson methods.

### Part C: Integration (Forecast-Driven Pricing)
*   **Pipeline:** Feeds the rough-volatility forecast as the `sigma` input for pricing.
*   **Sensitivity:** Compares pricing impacts ($ and %) across historical, GARCH, and rough-volatility forecasts, mapping spreads across 13 moneyness levels and 4 maturities.

## 🛠️ Technology Stack
*   **Python:** `numpy`, `pandas`, `yfinance`, `arch`, `scipy`, `scikit-learn`, `matplotlib`, `plotly`.

## 📈 Key Findings
1.  **Volatility Roughness:** Anti-persistence (H < 0.5) confirmed across all assets; rough volatility provides superior performance during market stress.
2.  **Model Hierarchy:** RV-based models (HAR-RV and Rough Vol) outperform conditional variance models (GARCH/EGARCH).
3.  **Economic Impact:** Pricing models are highly sensitive to volatility inputs; model choice creates tradable pricing spreads, especially for short-dated, out-of-the-money options.

---
*Disclaimer: This repository is for educational and research purposes only and does not constitute financial or trading advice.*
