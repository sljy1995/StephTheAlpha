---
layout: post
title: "Studying the Daily Seasonality of EURUSD"
date: 2026-01-01
excerpt: ""
---

__All content here is for research and educational purposes only, not financial advice.__

# Studying the EURUSD

While intraday trends and monthly seasonality information on the EURUSD is widely available, it is worthwhile to understand the data better to see if there are intrinsic patterns that can be distilled for further studies to develop a trading strategy. 

In this article, we study the intraday trends of the EURUSD and compare it across the different trading days of the week to spot volatility regimes and daily seasonlity patterns.

### EURUSD Background

EURUSD indicates the amount of USD required to purchase one EUR. The EURUSD is the most traded currency pair globally, and has high liquidity, which enables tighter spreads as well as market depth. It first started trading in Jan 1999, when the EUR was introduced as the common currency for several European countries. 

## Preparing the Dataset

The 1-min EURUSD prices data across the range of 2024-2025 was obtained from Massive. We will use 2025’s data for analysis and conduct back tests on 2024 data.
The dataset is cleaned for duplicates and made to be time zone-aware, specifically with UTC time zone. It is also observed that there are missing data in the magnitudes of ~1-3, which is taken as omitted data due to low liquidity. After cleaning up, we have a total of 364,053 minutes worth of data for the year of 2025 that will be used for analysis. 

## Analysis of EURUSD in 2025

### Distribution of Daily EURUSD Returns 

We start the research with understanding the distribution of EURUSD log returns across different days of the week. 

<figure>
    <p align="center">
    <small><em>
      <u>Figure 1: Spread of Log Returns by Day (2025)</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/eurusd/weekday_plot.png" alt="Spread of Log Returns by Day" width="600">
  </p>
</figure>

<p align="center">
  <small><em><u>Table 1: Summary Statistics of EURUSD Log Returns by Days of the Week</u></em></small>
</p>

| Weekday   | n     | Mean        | Median | Std      | Skew      | Kurtosis | p05       | p95       | Hit Rate |
|-----------|-------|-------------|--------|----------|-----------|----------|-----------|-----------|----------|
| Monday    | 73,251 | 6.20e-07    | 0.0    | 0.000145 | 0.012425  | 33.04    | -0.000205 | 0.000205  | 0.4779   |
| Tuesday   | 72,241 | 2.01e-07    | 0.0    | 0.000137 | 0.202521  | 21.42    | -0.000204 | 0.000203  | 0.4760   |
| Wednesday | 73,201 | 2.95e-07    | 0.0    | 0.000154 | -0.252609 | 60.31    | -0.000211 | 0.000211  | 0.4774   |
| Thursday  | 73,141 | 4.12e-07    | 0.0    | 0.000149 | 0.005264  | 40.33    | -0.000213 | 0.000214  | 0.4770   |
| Friday    | 65,323 | -4.41e-07   | 0.0    | 0.000183 | -18.2796  | 1572.22  | -0.000211 | 0.000205  | 0.4794   |
| Sunday    | 6,895  | 6.58e-06    | 0.0    | 0.000373 | 12.9142   | 912.11   | -0.000198 | 0.000209  | 0.4721   |

We can observe that the log returns are centred close to 0 on all days, meaning there is negligible unconditional return bias. 

In particular, Sunday exhibits the highest volatility, with a standard deviation of 0.000373. The extreme outliers on Sundays are attributable to weekend opening price gaps, as information accumulated over the Saturday trading break are incorporated into prices at the market opening on Sundays. 

We can also observe that Friday has the largest standard deviation relative to other weekdays. Additionally, it also has the largest kurtosis (1572) and pronounced negative skew (-18.28), indicating stubstantial downside tail risk. it is likely that institutional participants rebalance or reduce exposure ahead of the weekend, increasing the probability of large price adjustments.

We move on to look at the intraday log returns.

<figure>
    <p align="center">
    <small><em>
      <u>Figure 2: Intraday Log Returns (2025)</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/eurusd/intraday_ret.png" alt="Intraday Log Returns for 2025" width="900">
  </p>
</figure>

Mean intraday returns exhibit no visually strong or persistent directional pattern across days, with mean returns remaining close to 0 across most hourly buckets. However, modest positive deviations can be observed across the 1200hrs to 1400hrs time period, particularly during mid-week. This coincides with the London-New York market hours overlap. In contrast, 2100hrs on Friday exhibits a pronounced negative mean.

### Intraday Volatility Analysis

Now that we've analysed the returns across days of the week and within the days, we move on to study volatility.

<figure>
    <p align="center">
    <small><em>
      <u>Figure 3: Intraday Volatility (2025)</u>
   </em></small>
  </p>
  <p align="center">
    <img src="/assets/img/eurusd/intraday_vol.png" alt="Intraday Volatility (2025)" width="900">
  </p>
</figure>

We can see that there are three regions of elevated volatility that largely tallies with ATFX's reporting of intraday volatility behaviour:
1. 0600hrs to 0900hrs, which coincides with the London open.
2. 1200hrs to 1500hrs, which coincides with the London-New York session overlap. In particular, Wednesday exhibits persistent elevated volatility beyond this period up till 2100hrs.
3. 2100hrs, particularly Fridays: likely reflecting end-of-day positioning effects, similarly for Friday with pre-weekend repositioning to reduce risk exposure. 

## Analysis of EURUSD in 2024



## Comparing Data Between 2024 and 2025




### Citations
ATFX. ‘Best Time to Trade EURUSD - Optimal Trading Hours Explained’. ATFX Global - Official Website, 28 August 2024. https://www.atfx.com/en/analysis/trading-strategies/best-time-to-trade-eurusd.

*PS: GenAI was used to support the writing of this piece - but mostly for equation writing, cleaning up of markdown formatting, and language!)*
