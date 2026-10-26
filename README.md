# NIFTY 50 Trading Volume Forecasting

Time-series forecasting of NIFTY 50 trading volume using historical market data and Prophet.

## Project Overview

This project treats NIFTY 50 trading volume as a financial time-series forecasting problem. It performs exploratory analysis, applies a chronological train/test split, fits a Prophet model with trend and seasonal components, evaluates the model on an out-of-sample 2025 holdout, and generates a 90-weekday forward forecast approximation with 90% prediction intervals.

## Features

- Download NIFTY 50 historical OHLCV data using `yfinance`
- Explore trading-volume trends and distribution
- Apply a log transformation to stabilize volume scale
- Use a chronological train/test split to avoid look-ahead bias
- Model weekly and yearly seasonality with Prophet
- Compare Prophet with naive and weekday-median baselines on the same holdout dates
- Evaluate forecasts using MAE, RMSE, WAPE, MAPE, and MASE
- Inspect residuals, seasonal components, and empirical prediction-interval coverage
- Optionally run walk-forward cross-validation
- Visualize actual vs predicted 2025 volume
- Generate a 90-weekday forward forecast approximation
- Visualize forecast uncertainty using prediction intervals

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- yfinance
- Prophet
- Jupyter Notebook

## Methodology

### 1. Data Collection

NIFTY 50 index data (`^NSEI`) is downloaded from Yahoo Finance. The project focuses on daily trading volume.

### 2. Preprocessing

Trading volume is transformed using:

```text
log_volume = log(1 + Volume)
```

This reduces the effect of large scale differences in the raw volume series.

### 3. Train/Test Design

All observations through December 2024 are used for model training. Calendar-year 2025 is held out as an out-of-sample test period.

### 4. Forecasting Model

Prophet is configured with:

- Yearly seasonality
- Weekly seasonality
- No daily seasonality
- 90% prediction intervals

### 5. Evaluation Metrics

The model is evaluated using:

- **MAE:** Mean Absolute Error
- **RMSE:** Root Mean Squared Error
- **MAPE:** Mean Absolute Percentage Error

## Evaluation and Results

The notebook now evaluates the 2025 chronological holdout while retaining flagged low/zero-volume observations, compares Prophet against a fixed-origin naive forecast and a weekday-median baseline, and reports MAE, RMSE, WAPE, MAPE, and MASE. It also includes residual diagnostics, empirical prediction-interval coverage, Prophet component plots, and an optional walk-forward cross-validation cell.

**Reproduce the results:** Open `notebooks/nifty50_volume_forecasting.ipynb`, run all cells from top to bottom, and use the newly generated metric tables. Previous saved numbers are not reproduced here because they were generated under the earlier filtering approach and should not be compared directly with the updated evaluation.

The 90-day forward forecast uses 90 weekdays as an approximation; it does not automatically remove NSE exchange holidays. Forecasts are educational time-series estimates and are not investment recommendations.

## Project Structure

```text
NIFTY-50-Time-Series-Forecasting/
│
├── notebooks/
│   └── nifty50_volume_forecasting.ipynb
│
├── requirements.txt
└── README.md
```

## Disclaimer

This project is for educational and research purposes only and does not constitute financial advice or an investment recommendation.
