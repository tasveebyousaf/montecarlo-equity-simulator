# 📈 Monte Carlo Stock Price Simulation — MSFT

> Simulate Microsoft's future stock price using **Geometric Brownian Motion** and 1,000 Monte Carlo paths, calibrated on real historical data via `yfinance`.

---

## About

This project downloads 3 years of MSFT historical price data, calibrates a Geometric Brownian Motion (GBM) model from empirical log-returns, and projects 1,000 simulated price paths 252 trading days into the future. It calculates expected final price, standard deviation, 95% Value at Risk, and probability of profit — all in a single, beginner-friendly Python file. The simulation uses the exact GBM discretisation for theoretically consistent log-normal price distributions. Output is a two-panel chart: historical prices on the left, simulated paths with a 90% confidence band on the right.

---

## Quickstart

### ▶ Google Colab (no setup needed)

1. Open a new notebook at [colab.research.google.com](https://colab.research.google.com)

2. Paste or upload `monte_carlo_msft.py` into a code cell and run it.

### 💻 Local Python

```bash
# 1. Install dependencies
pip install yfinance matplotlib numpy pandas

# 2. Run
python monte_carlo_msft.py
```

**Python 3.9+** recommended.

---

## Output

| Panel | Description |
|-------|-------------|
| **Left** | Historical adjusted closing price (3 years) |
| **Right** | 1,000 simulated price paths with median and 90% confidence band |

A chart is saved as `monte_carlo_msft.png` in the working directory.

Console output:
```
Starting price : $420.00
Expected price : $498.31
Std deviation  : $112.45
95% VaR floor  : $298.10
Prob(profit)   : 68.40%
```

---

## Key Insights

- **GBM is a baseline, not a forecast.** It assumes constant drift and volatility — useful for understanding price uncertainty, not for predicting direction.
- **Drift dominates long horizons.** Small changes in μ compound significantly over 252 days; uncertainty (σ) fans out the path distribution.
- **VaR is model-dependent.** Because GBM assumes thin-tailed normal log-returns, it will underestimate the probability of extreme losses vs. real markets.
- **More paths = more stable estimates.** At 1,000 simulations the metrics are stable; increasing to 10,000 smooths the distribution further at minimal compute cost.

---

## Limitations

| Limitation | Potential upgrade |
|------------|-------------------|
| Constant volatility | GARCH or Heston model |
| Thin tails (normal returns) | Jump-diffusion (Merton model) |
| No mean-reversion | Ornstein–Uhlenbeck process |
| Single asset | Cholesky multi-asset GBM |

---

## Dependencies

```
yfinance
numpy
matplotlib
pandas
```

---

## Project Structure

```
monte_carlo_msft.py   ← single-file simulation (all logic + plots)
monte_carlo_msft.png  ← generated chart (created on first run)
README.md
```

---

*For educational purposes only. Not financial advice.*
