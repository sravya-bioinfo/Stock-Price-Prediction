# Stock Price Prediction
**Industry:** Finance | **Domain:** AI & ML | **Tools:** Python, Pandas, TensorFlow/Keras, Matplotlib

---

## Project Overview

This project predicts future stock closing prices using historical price data and technical indicators. An **LSTM (Long Short-Term Memory)** neural network learns temporal patterns in price time-series to forecast the next trading day's closing price.

---

## Folder Structure

```
stock_price_prediction/
├── stock_price_prediction.py    ← Main script (all steps)
├── stock_prediction_plot.png    ← Generated visualization (after running)
└── README.md                    ← This file
```

---

## Dataset

**Option 1 — Yahoo Finance (Recommended):**
```bash
pip install yfinance
```
The script automatically downloads data for the configured ticker (default: `AAPL`).

**Option 2 — Kaggle Stock Data:**  
🔗 https://www.kaggle.com/datasets/camnugent/sandp500

> If neither is available, the script generates synthetic data using Geometric Brownian Motion so you can still run and demonstrate the model.

---

## How to Run

### 1. Install dependencies

**Minimum (no TensorFlow):**
```bash
pip install pandas numpy scikit-learn matplotlib
```

**Full (with LSTM):**
```bash
pip install pandas numpy scikit-learn matplotlib tensorflow yfinance
```

### 2. Configure the ticker (optional)
Edit the top of `stock_price_prediction.py`:
```python
TICKER     = "AAPL"        # Change to any stock symbol
START_DATE = "2018-01-01"
END_DATE   = "2023-12-31"
```

### 3. Run
```bash
python stock_price_prediction.py
```

---

## Pipeline Steps

| Step | Description |
|------|-------------|
| 1 | **Load Data** — Yahoo Finance API or synthetic GBM data |
| 2 | **Indicators** — Compute SMA-20, SMA-50, RSI-14 |
| 3 | **Preprocess** — Normalize with MinMaxScaler, create 60-day sequences |
| 4 | **Train LSTM** — Stacked LSTM (128 → 64 → Dense) with early stopping |
| 5 | **Evaluate** — RMSE, MAPE, directional accuracy backtest |
| 6 | **Visualize** — Actual vs Predicted, Moving Averages, RSI chart (saved as PNG) |

---

## Key Concepts

- **LSTM (Long Short-Term Memory):** A type of recurrent neural network that can learn long-range dependencies in sequential data — ideal for time-series like stock prices.
- **Technical Indicators:**
  - **SMA (Simple Moving Average):** Smooths price data to identify trends.
  - **RSI (Relative Strength Index):** Measures momentum. RSI > 70 = overbought, RSI < 30 = oversold.
- **RMSE (Root Mean Squared Error):** Average prediction error in original dollar units — lower is better.
- **Backtest:** Simulates trading based on model predictions to measure real-world direction accuracy.

---

## Sample Output

```
══════════════════════════════════════════════════
  MODEL EVALUATION RESULTS
══════════════════════════════════════════════════
  RMSE : $3.47  (avg prediction error in dollars)
  MAPE : 1.89%  (mean absolute percentage error)
══════════════════════════════════════════════════

  Backtest — Direction Accuracy: 54.3%
  (Predicted the correct direction 152/280 times)
```

A plot `stock_prediction_plot.png` is also saved showing:
- Actual vs. Predicted prices (test period)
- Historical prices with SMA-20 and SMA-50
- RSI indicator with overbought/oversold zones

---

## Extending the Project

- **Try GRU** (Gated Recurrent Unit) — faster to train, similar accuracy
- **Add more features** — MACD, Bollinger Bands, sentiment from news
- **Multi-step forecasting** — predict 5 or 30 days ahead
- **Portfolio optimization** — apply predictions across multiple tickers

---

## Disclaimer

> This project is for educational purposes only. Stock price predictions are not financial advice and should not be used for real trading decisions.

---

## Author

AI & ML Internship Project — Stock Price Prediction  
Dataset: Yahoo Finance API / Kaggle
