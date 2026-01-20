---
layout: default
title: "Monetising Volatility Risk Premium for AAPL, Part III: Hedging with a Put Spread"
date: 2026-01-12
excerpt:"We studied how a put spread helps preserve exposure to VRP monetisation while capping downside risk by dampening gamma-driven convexity, and examined how the PnL distribution is altered from a naked put. In particular, we derived that a long put with a -0.25 delta presented the optimal risk-adjusted performance, as shown by a reduction in risk-related metrics, and an increase by ~300% in the Sharpe ratio."
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

Lower-delta puts (e.g. -0.10) correspond to deeper out-of-the-money strikes and therefore carry lower premiums, thereby preserving a larger proportion of the VRP collected by the short put. These lower-delta puts provide protection against extreme market dislocations, but offer limited mitigation against moderate drawdowns. 

In contrast, higher-delta puts (e.g. -0.30) are closer to the ATM short puts and absorb losses earlier to substantially reduce tail-risk amplification, however this comes at the cost of lower net premium income collected.

Therefore, by analysing this range of deltas for the long put, we can evaluate the corresponding trade-offs between net premium capture and risk mitigation to identify the most adequate delta to select the long put at.

## Understanding how the Put Spread Impacts Delta and Gamma Exposures

### Net Delta of the Put Spread

$$
\Delta_{\text{spread}} = \Delta_{\text{short}} + \Delta_{\text{long}}
$$

where  
- $\Delta_{\text{short}} < 0$ is the delta of the short ATM put  
- $\Delta_{\text{long}} < 0$ is the delta of the long OTM protective put  

$$
\Delta_{\text{spread}} = (-1)\Delta_{\text{short}} + (+1)\Delta_{\text{long}}
$$

Therefore, the long put has the effect of reducing the overall delta of the put spread. 

### Net Gamma of the Put Spread

$$
\Gamma_{\text{spread}} = (-1)\Gamma_{\text{short}} + (+1)\Gamma_{\text{long}}
$$

Both puts have positive gamma. The long put offsets the negative convexity of the short position. As the hedge delta increases (moves closer to ATM), $\Gamma_{\text{long}}$ increases, reducing net short gamma.

This term dominates during large market moves and generates tail-risk in naked short puts.

## Performance of Put Spreads Across Long Put Deltas

We study the performance of put spreads across the range of long put deltas from -0.30 to -0.10 inclusive. 
  
  <p align="center">
    <small><em><u>
      Table 1: Summary Statistics of Different Hedge Deltas
    </u></em></small>
  </p>

| Strategy | Hedge Delta | Trades | Mean PnL | Std Dev | Skew | VaR 99% | ES 99% | Worst Loss | Total PnL |
|---------|------------:|-------:|---------:|--------:|-----:|--------:|-------:|-----------:|----------:|
| Naked Put | — | 341 | 40.45 | 332.92 | -1.53 | -1025.91 | -1139.38 | -1315.00 | 13,792 |
| Put Spread | -0.10 | 64 | 53.17 | 304.60 | -1.39 | -822.31 | -870.50 | -870.50 | 3,403 |
| Put Spread | -0.15 | 150 | 32.50 | 286.52 | -1.42 | -879.67 | -958.75 | -968.50 | 4,875 |
| Put Spread | -0.20 | 150 | 29.56 | 261.86 | -1.50 | -820.42 | -888.75 | -949.00 | 4,434 |
| Put Spread | -0.25 | 147 | 29.24 | 234.87 | -1.56 | -757.70 | -896.25 | -940.50 | 4,298.5 |
| Put Spread | -0.30 | 87 | 44.32 | 210.06 | -1.82 | -543.61 | -940.50 | -940.50 | 3,855.5 |

We note that the number of trades for deltas -0.10 and -0.30 are based on substantially smaller sample sizes (<100) and therefore provide less reliable estimates of the distribution, so we drop them to only study the reliable regions with ~150 trades.

#### Tail-risk Mitigation
We observe that all deltas were effective in improving the tail-risk magnitude, seen from the reduction of ES99 from -1139 USD to the range of -890 to -960 USD. Likewise, the worst-case losses are also capped from -1315 USD to a range of -970 to -940 USD. It is worth noting that all skew values remain negatively skewed across deltas, indicating that convexity risk is dampened but not eliminated - this is consistent with what we should theoreticially expect.

#### Volatility of PnL
There is a clear monotonic trend, where the standard deviation of PnLs reduce as the (absolute) hedge delta increases. This is consistent with the greeks-based interpretation above where we decomposed how the put spread's gamma is reduced with the long put offsetting as its strike price gets closer to ATM (or as absolute hedge delta increases). 

  <p align="center">
    <small><em><u>
      Table 2: Sharpe Ratio for Different Hedge Deltas
    </u></em></small>
  </p>
| Strategy                | Delta | Sharpe Ratio (rf = 3%) |
|-------------------------|-------|------------------------|
| Long Put (Put Spread)   | -0.15 | 0.1380                 |
| Long Put (Put Spread)   | -0.20 | 0.1388                 |
| Long Put (Put Spread)   | -0.25 | 0.1626                 |
| Naked Put               |  —    | 0.0622                 |


Among the long put configurations considered, **−0.25 delta** presents as the choice with highest risk-adjusted performance as measured by the Sharpe ratio. 

## Conclusion

This study demonstrates that a pure naked put strategy can serve as a baseline approach for monetising VRP through trading AAPL options, but it is accompanied by pronounced downside tail risk driven by delta and gamma exposures. Through an examination the associated risks, we show that incorporating a long put effectively attenuates these tail risks. Among the configurations considered, a −0.25 delta long put provides the most favourable trade-off, offering meaningful dampening of extreme downside outcomes while preserving the ability to monetise VRP.

