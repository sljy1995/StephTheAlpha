---
layout: default
title: "Monetising Volatility Risk Premium for AAPL"
date: 2025-12-25
summary: "We examine the persistence of AAPL’s volatility risk premium and show how it can be converted into a systematic put-selling signal for retail traders."
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

We use OptionMetric's Ivy DB US Option Volatility Surface dataset to derive the annualised IV from 10DTE near-ATM AAPL put options (Δ ≈ −0.50), and corresponding AAPL spot prices from Centre for Research in Security Prices (CRSP) datasets to derive the annualised RV over 7 trading days rolling windows.

### Citations
Feunou, B., Lopez Aliouchkin, R., Tédongap, R., & Xi, L. (2017). Variance premium, downside risk and expected stock returns (No. 2017-58). Bank of Canada. 
