---
layout: default
title: "Monetising Volatility Risk Premium for AAPL"
date: 2025-12-25
excerpt: "The persistence of AAPL’s volatility risk premium was studied and  converted into a systematic put-selling signal for retail traders. Over a period of 2.5 years, the strategy was able to generate a total of USD 13,745.50 with one contract traded per execution, with a max drawdown of USD 8071.50. Assuming a portfolio capital of USD50,000 for a beginner to intermediate retail trader, the Sharpe ratio is 1.65, assuming a risk-free rate of 3%."
---
# Monetising Volatility Risk Premium for AAPL 

Volatility Risk Premium (VRP) refers to the difference between the Implied Volatility (IV), that is forward-looking and derived from option prices, and the Realised Volatility (RV) that is the actual variance that is realised over time (Feunou, 2017). A common observation is that IV is usually larger than RV, which indicates opportunity to capitalise on the premium from the difference between IV and RV, which is the VRP. 

$$
\mathrm{VRP} \equiv \mathrm{IV} - \mathrm{RV}
$$

For this series of VRP-type strategy research, we start with studying a large-cap stock, Apple (Ticker: AAPL), with relevant datasets are provided by Wharton Research Data Services (WRDS). We study its VRP to derive a basic signal for a corresponding Put Option strategy that is viable for a retail trader. In a subsequent series, we then study the risk management measures as well as other possible strategies. 

## Using 10DTE  AAPL Options 

For this study, we anchor our parameters using AAPL put options of ~10DTE (10 Calendar Days / 7 Trading Days), with a __hard minimum of 8DTE and maximum of 12DTE__, with the following reasons:

1.   __Liquidity__: 10DTE options present sufficient liquidity for a more optimal bid-ask spread as well as sufficient order-book depth. This ensures fill quality, reduces slippage, and is realistically testable and executable.
2.   __Dampened Gamma Risks__: 10DTE options exhibit materially lower gamma exposure than short-dated contracts, reducing gamma-driven PnL variability, and allowing theta decay to remain a more meaningful and systematic contributor to the overall strategy returns.

The date range for the data that we study is between __1 Jun 2022 and 31 Dec 2024__, or what I categorise as __Post-COVID-19 Regime__. 

## Derivation of IV and RV

We use OptionMetric's Ivy DB US Option Volatility Surface dataset to derive the annualised IV from 10DTE near-ATM AAPL put options (Δ ≈ −0.50), and corresponding AAPL spot prices from Centre for Research in Security Prices (CRSP) datasets to derive the annualised RV over 7 trading days rolling windows. Thereafter, the VRP is derived.

### 7-Day Annualised RV

$$
\begin{aligned}
r_t &= \frac{P_t - P_{t-1}}{P_{t-1}
}
\qquad\qquad
\mathrm{RV}_t^{(7)} &= \sqrt{\frac{252}{7} \sum_{i=0}^{6} r_{t-i}^2}
\end{aligned}
$$

<figure>
    <p align="center">
    <small><em>
      <u>Figure 1: Volatility Risk Premium for AAPL (IV − RV)</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/vrp.png" alt="AAPL VRP" width="260">
  </p>
  
</figure>


<figure>
    <p align="center">
    <small><em>
      <u>Figure 2: VRP Over Time</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/aapl_vrp.png" alt="AAPL VRP" width="600">
  </p>
  
</figure>
### Citations
Feunou, B., Lopez Aliouchkin, R., Tédongap, R., & Xi, L. (2017). Variance premium, downside risk and expected stock returns (No. 2017-58). Bank of Canada. 
