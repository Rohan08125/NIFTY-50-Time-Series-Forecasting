# NIFTY 50 Trading Volume Forecasting

Time-series forecasting of NIFTY 50 trading volume using historical market data and Prophet.

## Project Overview

This project treats NIFTY 50 trading volume as a financial time-series forecasting problem. It performs exploratory analysis, applies a chronological train/test split, fits a Prophet model with trend and seasonal components, evaluates the model on an out-of-sample 2025 holdout, and generates a 90-business-day forward forecast with 90% prediction intervals.

## Features

- Download NIFTY 50 historical OHLCV data using `yfinance`
- Explore trading-volume trends and distribution
- Apply a log transformation to stabilize volume scale
- Use a chronological train/test split to avoid look-ahead bias
- Model weekly and yearly seasonality with Prophet
- Evaluate forecasts using MAE, RMSE, and MAPE
- Visualize actual vs predicted 2025 volume
- Generate a 90-business-day forward forecast
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

## Results

The notebook computes the 2025 out-of-sample MAE, RMSE, and MAPE directly from the downloaded data and prints them in the **Key Results** section. It also produces a 90-business-day forward forecast after refitting the model on all available observations.

Results are intentionally generated at runtime because Yahoo Finance data can change as historical data is revised or new observations become available.

## Disclaimer

This project is for educational and research purposes only and does not constitute financial advice or an investment recommendation.
