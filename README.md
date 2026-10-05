# Momentum Factor Research - Indian Equities

## Overview

This project investigates whether **medium-term price momentum predicts next-month cross-sectional stock returns** among a fixed universe of large Indian listed companies.

The research tests **3-month, 6-month, 9-month and 12-month momentum formation horizons** and evaluates the signal using:

- Spearman **Rank IC**
- Quintile portfolio returns
- **Q5 − Q1** long-short spread
- One-sample t-tests
- Yearly Rank IC stability
- Cross-sectional regression beta

The project is designed as a compact example of a **quantitative equity research workflow**, rather than as a live trading strategy.

## Research workflow

```text
Hypothesis
   ↓
Download adjusted prices
   ↓
Validate + clean data
   ↓
Convert to month-end prices
   ↓
Construct momentum signal
   ↓
Calculate next-month returns
   ↓
Rank IC analysis
   ↓
Quintile portfolio test
   ↓
Q5 − Q1 spread
   ↓
Statistical significance
   ↓
Stability + interpretation
```

## Research question

> Does higher past momentum predict higher next-month returns across Indian equities?

### Null hypothesis

For both Rank IC and the Q5 − Q1 spread:

**H₀: Mean result = 0**

The project uses a two-sided one-sample t-test at the 5% significance level.

## Data

- **Source:** Yahoo Finance via `yfinance`
- **Frequency:** Daily prices converted to month-end prices
- **Sample:** March 2021 – August 2026
- **Universe:** 49 large Indian listed companies
- **Price field:** Adjusted prices (`auto_adjust=True`)

## Methodology

### 1. Momentum

For a formation horizon of `N` months:


Momentum_t = P_t/P_(t-N) - 1


### 2. Forward return


ForwardReturn_(t+1) = P_(t+1)/P_t - 1


### 3. Rank IC

Each month, stocks are ranked by momentum and the **Spearman correlation** between momentum and next-month returns is calculated.

### 4. Quintile portfolios

Stocks are sorted into five groups:

- Q1 = lowest momentum
- Q2
- Q3
- Q4
- Q5 = highest momentum

The long-short factor spread is:

\[
Q5-Q1
\]

## Results

Run the notebook to generate the current results. The final dashboard reports:

| Metric | Purpose |
|---|---|
| Mean Rank IC | Average cross-sectional predictive relationship |
| IC t-stat | Statistical significance of Rank IC |
| Mean Q5-Q1 | Long-short momentum spread |
| Spread t-stat | Statistical significance of the spread |
| Negative IC % | Frequency of months with negative IC |
| Mean Beta | Cross-sectional return sensitivity to momentum |

## Project structure

```text
momentum-factor-research/
│
├── momentum_factor_research.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Installation

```bash
git clone <your-repository-url>
cd momentum-factor-research
pip install -r requirements.txt
jupyter notebook
```

## Requirements

```text
numpy
pandas
yfinance
matplotlib
scipy
jupyter
```

## Limitations

This is research/education code, not investment advice.

Important limitations include:

- Fixed universe → potential survivorship bias
- Public Yahoo Finance data → not a point-in-time institutional dataset
- No transaction costs or market impact
- No turnover modelling
- Equal-weighted quintile portfolios
- Relatively short sample for factor research
- No out-of-sample validation in the current version

## Future improvements

The next version could test:

- sector-neutral momentum
- market-cap weighting
- transaction costs
- turnover
- volatility scaling
- value + quality factors
- multi-factor combination
- walk-forward / out-of-sample testing
- benchmark-relative performance
- drawdown and risk-adjusted metrics

## Disclaimer

This repository is for educational and research purposes only. It does not constitute investment advice, a recommendation, or an offer to buy or sell securities.
