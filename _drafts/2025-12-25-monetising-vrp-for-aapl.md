---
layout: default
title: "Monetising Volatility Risk Premium for AAPL, Part III: Hedging with a Put Spread"
date: 2026-01-12
---
<figure>
  <p align="center">
    <img src="/assets/img/put_spread.png" alt="Put Spread" width="600">
  </p>
</figure>

In the previous parts, we explored how VRP could be monetised through sort put writing, and examined the associated risk profile through a decomposition of the Greeks using Ito's formula. We also showed that while positive VRP as a signal to write puts generated positive PnL, the PnL distribution was dominated by Delta and Gamma risks, with Delta driving directonal risks, while Gamma drove tail-risk amplification.

In this series, we extend the study by introducing a risk hedging options structure: a put spread. By pairing the short At-the-Money (ATM) put with a long ATM protective put, the put spread preserves exposure to VRP monetisation, while capping downside risk and dampening gamma-driven convexity. We then examine how the put spread alters the PnL distribution, in particular the trade-off between premium income and tail-risk protection, providing a more palatable approach to harvest the VRP.

## Constructing the Put Spread
To construct the put spread, we extract the range of long protective puts of deltas in the ranges of 0.10 to 0.30 from OptionMetrics. From the risk management perspective, using delta as the selection criteria allows us to consider the suitability of the long puts with consideration for moneyness as well as downside convexity. 

Lower-delta puts (e.g. -0.10) correspond to deeper out-of-the-money strikes and therefore carry lower premiums, thereby preserving a larger proportion of the VRP collected by the short put. These lower-delta puts provide protection against extreme market dislocations, but offer limited mitigation against moderate drawdowns. Therefore, an analysis of the delta of the long put that will provide adequate hedge against the risks while preserving premium income is required.
