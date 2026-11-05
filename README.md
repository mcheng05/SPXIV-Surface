# Implied Volatility Surface from SPX Options

## Project Overview

This project focuses on constructing a continuous implied volatility surface from discrete S&P 500 index (SPX) options data.

Using historical options data from OptionsDX, we examine implied volatility across different strike prices and expiration dates. We apply the Black–Scholes pricing framework and numerical root-finding methods to estimate implied volatilities from observed market prices.

The primary objective is to use the **Stochastic Volatility Inspired (SVI) model** to fit smooth implied volatility smiles to the discrete observations and construct a continuous implied volatility surface across moneyness and time to maturity.

## Data

The analysis uses SPX options data from four selected trading days in 2023.

| Quarter | Date | Observations |
|---|---|---:|
| Q1 | January 4, 2023 | 9,940 |
| Q2 | June 30, 2023 | 10,272 |
| Q3 | August 15, 2023 | 10,104 |
| Q4 | November 14, 2023 | 10,387 |
| **Total** | | **40,703** |

The main quarterly analysis applies the following filters:

- Positive bid prices
- Implied volatility no greater than 100%
- Moneyness (strike / underlying price) between 0.75 and 1.25
- Days to expiration no greater than 365

Earlier exploratory analyses may use different filtering criteria.

## Methodology

### 1. Data Cleaning and Preparation

Historical SPX options data is cleaned and filtered to remove unsuitable observations. The resulting datasets are organized by quarter for further analysis.

### 2. Implied Volatility Estimation

The Black–Scholes pricing model is used to calculate implied volatility from observed option prices.

Numerical methods explored include:

- Bisection
- Newton–Raphson
- Brent's method

These methods allow us to estimate implied volatility at discrete combinations of strike price and maturity.

### 3. Exploratory Data Analysis

We investigate the behavior of implied volatility across strikes and expiration dates, focusing on:

- Volatility smiles and skews
- Differences across expiration dates
- Implied volatility term structure
- Changes in volatility patterns across quarterly observations

### 4. SVI Modeling and Volatility Surface Construction

The central modeling component of the project uses the **Stochastic Volatility Inspired (SVI) parameterization** to transform discrete implied volatility observations into smooth volatility smiles.

SVI models total implied variance as a function of log-forward moneyness:

\[
w(k)=a+b\left[\rho(k-m)+\sqrt{(k-m)^2+\sigma^2}\right]
\]

where:

- \(w(k)\) is total implied variance.
- \(k\) is log-forward moneyness.
- \(a,b,\rho,m,\sigma\) are model parameters.

By calibrating the SVI parameters to observed implied volatilities at different maturities, we aim to obtain smooth volatility smiles across strike prices.

Combining these fitted smiles with interpolation across maturities allows us to construct a continuous implied volatility surface.

### 5. Interest Rate and Term Structure Analysis

We also examine interest rate estimation using put–call parity and investigate the relationship between implied rates, maturity, and observed option prices.

## Repository Structure

- **`data/`** — Raw, intermediate, and filtered SPX options datasets organized by quarter.
- **`notebooks/`** — Exploratory analysis, implied volatility estimation, and term structure analysis.
- **`scripts/`** — Python scripts for OptionsDX data cleaning and implied interest rate calculations.
- **`src/`** — Supporting Python and R scripts.
- **`results/`** — Saved analysis outputs and figures.
- **`helpful-docs/`** — Mathematical background and Black–Scholes PDE derivations.

## Main Analysis Notebooks

- **`eda_quarterly_unified_iv_bisection.ipynb`** — Quarterly implied volatility analysis using bisection.
- **`iv_inversion_newton_brent.ipynb`** — Numerical implied volatility estimation using Newton–Raphson and Brent's method.
- **`term_analysis.ipynb`** — Term structure analysis and interest rate comparisons.

Other notebooks document preliminary analysis and intermediate stages of the project.

## Tools and Libraries

The project primarily uses Python and Jupyter Notebook, with supporting R code.

Key Python libraries include:

- NumPy
- pandas
- SciPy
- Matplotlib
- statsmodels

## Project Status

The main branch consolidates the group's data cleaning, exploratory analysis, implied volatility estimation, and interest rate analysis.

SVI calibration and continuous volatility surface construction form the central modeling objective of the project. SVI-related development may remain on separate branches while the implementation is being finalized.
