# Time-Series-Analysis-Python-Internship
Python project for internship: Analyze a stock price time-series dataset to detect trends, seasonality, and apply moving average smoothing using pandas, matplotlib, and statsmodels.
# Time Series Analysis - Internship Task

## Description
This project is part of my internship tasks. It focuses on analyzing a **time-series dataset** (stock prices) to detect trends, seasonality, and apply smoothing techniques. The analysis uses **Python**, **pandas**, **matplotlib**, and **statsmodels**.

---

## Objectives
- Plot time-series data and visually identify patterns.
- Decompose the series into **trend**, **seasonality**, and **residuals** using **statsmodels**.
- Perform **moving average smoothing** and plot the results.

---

## Dataset
The dataset used is **stock prices** with `Date` and `Close` columns.  
- The `Date` column is used as the index.  
- `Close` represents the stock closing price for each date.

Steps / Methodology
1. Load the dataset
```Python
import pandas as pd

df = pd.read_csv("Data Set For Task/stock_prices.csv")
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)

print(df.head())
```
2. Plot the time-series
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12,6))
plt.plot(df['Close'], label='Closing Price')
plt.title('Stock Prices Over Time')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.show()
```

3. Decompose the series
```python
from statsmodels.tsa.seasonal import seasonal_decompose

decomposition = seasonal_decompose(df['Close'], model='additive', period=30)
decomposition.plot()
plt.show()
```
4. Apply Moving Average Smoothing
```python
df['MA_7'] = df['Close'].rolling(window=7).mean()
df['MA_30'] = df['Close'].rolling(window=30).mean()

plt.figure(figsize=(12,6))
plt.plot(df['Close'], label='Original')
plt.plot(df['MA_7'], label='7-day MA')
plt.plot(df['MA_30'], label='30-day MA')
plt.title('Moving Average Smoothing')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.show()


