---
layout: default
title: "Monetising Volatility Risk Premium for AAPL, Part II: Risk Analysis of the Naked Put Strategy"
date: 2025-12-29
excerpt: "The persistence of AAPL’s volatility risk premium was studied and  converted into a systematic put-selling signal for retail traders. Over a period of 2.5 years, the strategy was able to generate a total of USD 13,745.50 with one contract traded per execution, with a max drawdown of USD 8071.50. Assuming a portfolio capital of USD50,000 for a beginner to intermediate retail trader, and a risk-free rate of 3%, the Sharpe ratio is 1.65. Of note, risk management measures have yet to been incorporated."
---
# Risk Analysis of a Naked Put Strategy with VRP>0 signal

## Recap/Background

In the previous part, we examined how there is opportunity to monetise VRP of AAPL using a simple VRP>0 signal. The simplest approach to it was to trade short puts and exit at around the half-life (~ 4 days)of the VRP decay lifetime. While this simple strategy was found to be profitable and regime-resilient, the residual risks had not been assessed. 

For naked puts, the downside risks can be hefty, and one extreme event could wipe out the many small wins from this strategy, or worse, multiple of such events could even result in an overall loss. It is therefore important to analyse the corresponding risks of this strategy, and implement hedges against them. 

## Examining the Tail Risks

We first visualise the spread of the PnL to understand the extent of tail risk associated with this strategy. 

<figure>
    <p align="center">
    <small><em>
      <u>Figure 1: Distribution of PnL</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/nd_pnl.png" alt="PnL Distribution" width="420">
  </p>
  
</figure>

<div align="center">

| Metric | Value |
|------|------:|
| Number of trades | 341 |
| Mean PnL | 40.45 |
| Median PnL | 160.00 |
| Standard deviation | 332.92 |
| Maximum PnL | 643.50 |
| Minimum PnL | -1,315.00 |
| Skewness | -1.53 |
| Excess kurtosis | 2.30 |
| Tail dominance (worst 5%) | 0.31 |

</div>

The distribution deviates substantially from normality, exhibiting strong negative skew and excess kurtosis, reflecting the asymmetric tail risk. 



### Fun Fact: The Signal Could Be Redundant:

