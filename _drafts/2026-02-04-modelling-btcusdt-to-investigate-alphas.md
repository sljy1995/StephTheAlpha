---
layout: post
title: "Modelling BTCUSDT to Investigate Alphas - Part I: Analysing BTCUSDT Volatility"
date: 2026-02-04
excerpt: ""
---
__All content here is for research and educational purposes only, not financial advice.__

# Introduction

## Why is BTCUSDT Worth Studying?
Cryptocurrency, because of its 24/7 continuous trading nature, presents different volatility clustering and gap dynamics. Within the cryptocurrency universe of traded pairs, BTCUSDT is the most traded, and serves as a natural benchmark to be studied. The accessibility of crypto perpetuals (perps) to retail traders provides leverage and the option to monetise convexity. Funding rates also presents as another form of risk premium that could be capitalised. These make BTCUSDT an ideal setting to study volatility, derivatives, and market microstructure. As BTC as a cryptocurrency continues to mature, it is observed that its volatility levels are also stabilising, having been at levels of ~80% in 2017 but decreasing to ~20% in 2024, and also being comparable to other mega-cap stocks like the Magnificent Seven (Wainwright, 2025).

## Statistical Analysis of BTCUSDT

From Binance, we obtained tick-level BTCUSDT spot trades from 17 Aug 2017 to 28 Jan 2026 with microsecond timestamp resolution, and aggregated them into one-minute intervals to analyse 1-min log-returns and 5-min log-volatility analysis. 

### Data Summary
  
<p align="center">
  <small><em><u>
    Table 1: Summary Statistics of 1-min Log Returns and 5-min Annualised Log Realised Volatility.
  </u></em></small>
</p>

| Metric        | Log Returns (1-min) | Log Realised Volatility (5-min, Ann.) |
|--------------|--------------------:|--------------------------------------:|
| Sample size  | 4,412,544           | 4,412,540                             |
| Mean         | 6.89e-07            | −1.008                                |
| Std. dev.    | 1.15e-03            | 0.985                                 |
| Minimum      | −0.0751             | −18.421                               |
| 25%          | −3.34e-04           | −1.518                                |
| Median       | 0.0000              | −0.990                                |
| 75%          | 3.35e-04            | −0.457                                |
| Maximum      | 0.0723              | 3.817                                 |

From the summary statistics, it can be seen that 1-min log returns exhibit a mean of approximately 0, as well as negligible unconditional drift and heavy tails. The 5-min realised volatility displays a wide dynamic range corresponding to distinct volatility regimes, with extremely low value reflecting period of minimal trading activity, and an upper tail corresponding to high-volatility regimes.

## HAR Model Estimation Results

**Dependent variable:** Future log realised volatility  
**Number of observations:** 3,528,880  

### Regression Coefficients

| Variable            | Coefficient | Std. Error | t-stat | p-value |
|---------------------|-------------|------------|--------|---------|
| Intercept           | -0.2196     | 0.001      | -413.8 | < 0.001 |
| log_rv_5m_ann       | 0.2169      | 0.001      | 396.9  | < 0.001 |
| log_rv_60m_ann      | 0.5738      | 0.001      | 549.6  | < 0.001 |
| log_rv_1440m_ann    | 0.1974      | 0.001      | 180.5  | < 0.001 |

### Model Fit

- R²: 0.496  
- Adjusted R²: 0.496  
- F-statistic: 1.16 × 10⁶ (p < 0.001)  
- Durbin–Watson: 0.517  

From the coefficients, it can be seen that the medium-horizon (1-hr) log RV dominates forecast dynamics with the largest coefficient of 0.5738. Nonetheless, the short and long-term horizons also contribute meaningfully. The coefficients are also highly statistically significant (all p-values < 0.001). 

Of note, the Durbin-Watson statistic (0.517) is < 2, indicating substantial residual autocorrelation that may not be well captured by the model, and may warrant further analysis and model extensions.

---

## Residual Diagnostics

- Skewness: -7.386  
- Kurtosis: 171.889  
- Jarque–Bera: 4.23 × 10⁹ (p < 0.001)  

Residuals exhibit extreme non-normality, reflecting jump risk and volatility clustering inherent in high-frequency crypto markets.

---

## Out-of-Sample Forecast Performance

- RMSE: 0.733  
- MAE: 0.420  
- MSE: 0.537  

### Relative Error Metrics

- Relative RMSE: 0.554  
- Relative MAE: 0.318  

The HAR model reduces forecast error by approximately 45% relative to a naive benchmark.


Residual diagnostics indicate strong short-run autocorrelation and pronounced conditional heteroskedasticity. We therefore augment the HAR mean equation with an AR(1) component and model the resulting innovations using a GARCH(1,1) specification with Student-t innovations. The estimated degrees of freedom indicate extremely heavy tails, consistent with high-frequency crypto market dynamics.



## Citations
Wainwright, Zack. ‘A Closer Look at Bitcoin’s Volatility’. Accessed 1 February 2026. https://www.fidelitydigitalassets.com/research-and-insights/closer-look-bitcoins-volatility.


