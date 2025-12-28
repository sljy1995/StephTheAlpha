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

We first examine the empirical distribution of the PnL to assess the magnitude and asymmetry of the tail risk associated with this strategy. 

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

  <p align="center">
    <small><em><u>
      Table 1: Summary Statistics of PnL
    </u></em></small>
  </p>

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

The distribution deviates substantially from normality, evidenced by its negative skewness (−1.53) and excess kurtosis (2.30), indicating asymmetric downside risk and fat-tailed loss behaviour. 

<div align="center">

  <p align="center">
    <small><em><u>
      Table 2: VaR and ES at 95% and 99% Confidence Levels
    </u></em></small>
  </p>

| Risk Metric | 95% Level | 99% Level |
|------------|----------:|----------:|
| Value-at-Risk (VaR) | -677.85 | -1025.91 |
| Expected Shortfall (ES) | -938.38 | -1139.38 |

</div>

Given the VaR estimates, the strategy’s losses are not expected to exceed USD 677.85 and USD 1,025.91 at the 95% and 99% confidence levels, respectively. Of note, the VaR estimates are computed on a per-trade basis given the strategy's trading approach. With the ES estimates, we can expect an average losses of USD 938.38 and USD 1139.38 conditional on the losses exceeding the respective VaR thresholds.

Nonetheless, while VaR and ES provide a measure of the extent of the risk, they do not explain the underlying causes for it.

## Delta and Gamma Risks

 Given a options-based strategy, it is necessary to analyse the Greeks and their associated risks. 

<div align="center">

  <p align="center">
    <small><em><u>
      Table 3: Overview of Greeks-associated Risks
    </u></em></small>
  </p>

 | Risk  | How it Affects Strategy's PnL | What this Greek Means? |
| ----- | ----------------------- |--------------------|
| Vega  | Primary *return* driver | Rate of change of option price given a change in IV |
| Theta | Income accrual          | Rate of change of option price given time decay|
| **Delta** | **Directional loss** | Rate of change of option price given change in underlying price |
| **Gamma** | **Tail amplification** | Rate of change of Delta given a change in underlying price |

 </div>

As a strategy built on monetising VRP, vega exposure primarily drives expected returns and is secondary to delta and gamma in driving extreme losses. In particular, a short put position carries positive delta, implying that profits increase as the underlying price rises and losses accrue as it falls. During sharp market declines, this directional exposure intensifies due to negative gamma, causing losses to accelerate non-linearly. We therefore focus our analysis on delta and gamma risks, which are the primary drivers of tail losses in naked put strategies.



This gives the motivation to incorporate appropriate risk management measures to hedge against the tail-risks, which could be larger than what is presented from our set of data, should extreme-case events occur.

### Fun Fact: The Signal Could Be Redundant:

