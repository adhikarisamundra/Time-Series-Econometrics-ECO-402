# Cycles, Not Trends: A Time Series Analysis of Canadian Lynx Population Dynamics

## Overview

This repository contains an applied time series econometrics analysis of the canonical `lynx` dataset, which records the annual number of Canadian lynx trapped from 1821 to 1934.

The project applies the complete Box–Jenkins methodology to demonstrate that the data is best characterized as a cyclical, trend-free, mean-reverting process driven by predator–prey dynamics, rather than a linear or randomly drifting trend.

---

## Repository Contents

### `lynx_analysis.R`
The core R script containing the full statistical pipeline. It:

- Generates all statistical models
- Performs diagnostic testing
- Automatically exports required visualizations as PDF files

### `paper.tex`
The LaTeX manuscript detailing:

- Theoretical background
- Econometric methodology
- Statistical interpretation of results

### Generated Plots (`.pdf`)
Running the R script automatically produces diagnostic and forecasting plots required for the paper, including:

- `fig_raw_series.pdf`
- `fig_moving_average.pdf`
- `fig_holt_winters.pdf`
- `fig_arma21_forecast.pdf`

---

## Methodology Pipeline

The analysis follows a structured Box–Jenkins workflow:

### 1. Exploratory Data Analysis (EDA)
Initial inspection of the 114-year dataset highlights:

- Extreme variance
- Strong cyclical behavior
- Dominant ~10-year oscillation

### 2. Trend and Decomposition
A 10-year centered moving average is applied to evaluate long-run structure and confirm the absence of a persistent linear trend.

### 3. Holt–Winters Smoothing
Holt–Winters exponential smoothing is fitted as a comparative benchmark to demonstrate the limitations of smoothing methods on strictly cyclical ecological data.

### 4. OLS and Feasible GLS Regression
Formal hypothesis testing is conducted for a deterministic linear time trend.

Because naive OLS residuals exhibit severe autocorrelation, a Generalized Least Squares (GLS) specification with AR(1) errors is estimated to obtain valid inference.

### 5. Stationary Transformations
The following transformations are applied:

- Log transformation to stabilize variance
- First differencing to stabilize the mean and remove integration

Stationarity is verified using the Augmented Dickey–Fuller (ADF) test.

### 6. ARMA Model Selection
Competing AR, MA, and ARMA specifications are compared using Akaike Information Criterion (AIC).

The preferred specification is identified as:

\[
ARMA(2,1)
\]

estimated on the differenced log-transformed series.

### 7. Forecasting
The final model is used to generate:

- 12-step-ahead forecasts
- 95% prediction intervals

The forecasts successfully reproduce the recurring ~10-year ecological cycle.

---

## Key Findings

### No Linear Trend
Both non-parametric smoothing and formal GLS regression indicate that the Canadian lynx population exhibits no statistically significant long-run linear trend over the sample period.

### ARMA(2,1) Superiority
The ARMA(2,1) model decisively outperforms competing specifications:

\[
\Delta AIC \approx 39
\]

relative to the next-best model.

Its complex autoregressive roots mathematically capture the approximately 9.6-year predator–prey cycle.

### Valid Inference Requires GLS
Naive OLS regressions produce invalid standard errors because the residuals are highly autocorrelated:

\[
\hat{\rho} \approx 0.82
\]

Feasible GLS is therefore necessary for statistically valid inference.

---

## Requirements and Execution

## Prerequisites

You will need:

### R Packages
Install the following R packages:

- `nlme` — Generalized Least Squares estimation
- `tseries` — Augmented Dickey–Fuller testing

### LaTeX Distribution
To compile the manuscript, install one of the following:

- TeX Live
- MiKTeX
- Overleaf (online)

---

## How to Run

### 1. Clone the Repository

```bash
git clone <repository-url>
