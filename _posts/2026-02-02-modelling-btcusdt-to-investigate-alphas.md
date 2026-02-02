---
layout: post
title: "Modelling BTCUSDT to Investigate Alphas - Part I: Forecasting BTCUSDT Volatility with a Heterogenous Autoregressive Model"
date: 2026-02-02
excerpt: "We used the 5 min, 1 hr, and 1 day realised volatilities (RV)  as coefficients to the Heterogenous Autoregressive (HAR) model to study the feasibility of forecasting RV at t + 5mins. While there was substantial residual autocorrelation observed that requires further treatment through model extensions, the HAR model was assessed to produce statistically superior results when compared to a naïve benchmark, reducing errors by ~20%."
---
__All content here is for research and educational purposes only, not financial advice.__

# Introduction

## Why is BTCUSDT Worth Studying?
Cryptocurrency, because of its 24/7 continuous trading nature, presents different volatility clustering and gap dynamics. Within the cryptocurrency universe of traded pairs, BTCUSDT is the most traded, and serves as a natural benchmark to be studied. The accessibility of crypto perpetuals (perps) to retail traders provides leverage and the option to monetise convexity. Funding rates also presents as another form of risk premium that could be capitalised. These make BTCUSDT an ideal setting to study volatility, derivatives, and market microstructure. As BTC as a cryptocurrency continues to mature, it is observed that its volatility levels are also stabilising, having been at levels of ~80% in 2017 but decreasing to ~20% in 2024, and also being comparable to other mega-cap stocks like the Magnificent Seven (Wainwright, 2025).

## Statistical Analysis of BTCUSDT

From Binance, we obtained tick-level BTCUSDT spot trades from 17 Aug 2017 to 28 Jan 2026 with microsecond timestamp resolution, and aggregated them into one-minute intervals to analyse 1-min log-returns and 5-min log Realised Volatility (RV) analysis. 

### Data Summary
  
<p align="center">
  <small><em><u>
    Table 1: Summary Statistics of 1-min Log Returns and 5-min Annualised Log RV.
  </u></em></small>
</p>

<div style="overflow-x: auto;">

| Variable / Statistic | Coeff | Std. Error | $t$-stat | $p$-value |
| :--- | :---: | :---: | :---: | :---: |
| **HAR (Log)** | | | | |
| Intercept | $-0.2196$ | $0.001$ | $-413.8$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{5m})$ | $0.2169$ | $0.001$ | $396.9$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{60m})$ | $0.5738$ | $0.001$ | $549.6$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{1d})$ | $0.1974$ | $0.001$ | $180.5$ | $< 0.001$ |
| **Residuals** | | | | |
| Skewness | $-7.386$ | — | — | — |
| Kurtosis | $171.889$ | — | — | — |
| Jarque–Bera | $4.23e9$ | — | — | $< 0.001$ |
| **Model Fit** | | | | |
| $R^2$ | $0.496$ | — | — | — |
| Adj. $R^2$ | $0.496$ | — | — | — |
| $F$-stat | $1.16e6$ | — | — | $< 0.001$ |
| Durbin-W | $0.517$ | — | — | — |

</div>

<figure>
    <p align="center">
    <small><em>
      <u>Figure 1: Distribution Graphs of Log-returns, RV (5min, annualised), and Log RV (5min, annualised).</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/btcusdt/logret_rv_logrv_plots.png" alt="Graphs of Log-ret, RV_5min, Log RV_5min" width="600">
  </p>

From the summary statistics, it can be seen that 1-min log returns exhibit a mean of approximately 0, as well as negligible unconditional drift and heavy tails. The 5-min RV displays a wide dynamic range corresponding to distinct volatility regimes, with extremely low value reflecting period of minimal trading activity, and an upper tail corresponding to high-volatility regimes.

With reference to figure 1, we can see that the RV is heavily right-skewed, indicating a majority of low-RV periods but episodic occurances of high-volatility spikes, which is expected of BTC market activity. With log transformation, we are able to reduce the skewness substantially to produce a more symmetrical, bell-shaped curve, which will facilitate modelling subsequently.

### HAR Model Estimation Results

We specify a heterogeneous autoregressive (HAR) model to analyse how RV at multiple horizons contributes to forecasting five-minute RV at t + 5min.

$$\text{RV}_{t+5}^{(5\text{min, ann})} = \beta_0 + \beta_{5min} \text{RV}_{t}^{(5\text{min, ann})} + \beta_{60min} \text{RV}_{t}^{(60\text{min, ann})} + \beta_{1d} \text{RV}_{t}^{(1\text{day, ann})} + \epsilon_{t+5}$$

The dataset was split into training and testing samples using a 80-20 split, with the model parameters estimated on the training set. From figure 1, we can see that there is a need to use Log-transformed RV instead to stabilise regression estimates by dampening the influence of extreme RV spikes on Ordinary Least Squares (OLS) estimation. 

**Dependent variable:** $\log(\text{RV}_{t+5}^{(5\text{min, ann})})$

**Number of observations:** 3,528,880  

#### Regression Coefficients, Model Fit, and Residual Diagnostics

<p align="center">
  <small><em><u>
    Table 2: Regression Coefficients of HAR Model.
  </u></em></small>
</p>

| Variable / Statistic | Coefficient | Std. Error | $t$-stat | $p$-value |
| :--- | :---: | :---: | :---: | :---: |
| **HAR Regression (Log)** | | | | |
| Intercept | $-0.2196$ | $0.001$ | $-413.8$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{(5\text{min, ann})})$ | $0.2169$ | $0.001$ | $396.9$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{(60\text{min, ann})})$ | $0.5738$ | $0.001$ | $549.6$ | $< 0.001$ |
| $\log(\text{RV}_{t}^{(1\text{day, ann})})$ | $0.1974$ | $0.001$ | $180.5$ | $< 0.001$ |
| | | | | |
| **Residual Diagnostics** | | | | |
| Skewness | $-7.386$ | — | — | — |
| Kurtosis | $171.889$ | — | — | — |
| Jarque–Bera | $4.23 \times 10^{9}$ | — | — | $< 0.001$ |
| | | | | |
| **Model Fit Statistics** | | | | |
| $R^2$ | $0.496$ | — | — | — |
| Adjusted $R^2$ | $0.496$ | — | — | — |
| $F$-statistic | $1.16 \times 10^{6}$ | — | — | $< 0.001$ |
| Durbin–Watson | $0.517$ | — | — | — |

The model explains a substantial extent of the forecasted $\widehat{\text{RV}}_{t+5}^{(5\text{min, ann})}$, as reflected in the R² value of 0.496. From the coefficients, it can be seen that the medium-horizon $\log(\text{RV}_{t}^{(60\text{min, ann})})$ dominates forecast dynamics with the largest coefficient of 0.5738. Nonetheless, the short and long-term horizons also contribute meaningfully. The coefficients are also highly statistically significant (all p-values < 0.001). 

Of note, the Durbin-Watson statistic (0.517) is < 2, indicating substantial residual autocorrelation that may not be well captured by the model, and may warrant further analysis and model extensions to refine the HAR model.

Residuals exhibit extreme non-normality, reflecting jump risk and volatility clustering inherent in high-frequency crypto markets.

### Model Performance on Test Sample

Out-of-sample (n = 882,220) forecast performance is evaluated using root mean squared error (RMSE) and mean absolute error (MAE).

#### Test Sample Forecast Performance

<p align="center">
  <small><em><u>
    Table 3: Absolute and Relative Error Metrics .
  </u></em></small>
</p>

| Metric | Value |
|--------|------:|
| Root Mean Squared Error (RMSE) | 0.733 |
| Mean Absolute Error (MAE) | 0.420 |
| Relative RMSE | 0.791 |
| Relative MAE | 0.789 |

It can be seen from the RMSE that large forecast errors exist, resulting in RMSE > MAE. The relative RMSE and MAE show that the model outperforms a naive benchmark, proving that the HAR model provides improved performance in capturing the volatility dynamics of BTCUSDT. The error metrics are then compared to that of a naïve benchmark:

$$\widehat{\text{RV}}_{t+5}^{(5\text{min, ann})} = \text{RV}_{t}^{(5\text{min, ann})}$$ 

Comparatively, it is notable that the relative RMSE and MAE show that the HAR model can reduce RV forecasting errors by ~20%.

## Conclusion

We find that a HAR model utilising realised volatility horizons at the 5-min, 1-hour, and 1-day levels provides a statistically meaningful approach to forecasting $\widehat{\text{RV}}_{t+5}^{(5\text{min, ann})}$, with performance superior to that of a naïve persistence benchmark.

In the next stage of this study, we will address the residual autocorrelation through further model extensions to improve our forecast accuracy, before progressing to a deeper analysis of how these volatility forecasts may be translated into monetisable trading opportunities.

## Citations
Wainwright, Zack. ‘A Closer Look at Bitcoin’s Volatility’. Accessed 1 February 2026. https://www.fidelitydigitalassets.com/research-and-insights/closer-look-bitcoins-volatility.

*PS: GenAI was used to support the writing of this piece - but mostly for equation writing, cleaning up of markdown formatting, and language!*
