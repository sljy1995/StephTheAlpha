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

## Basic Analysis of EURUSD in 2025
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

We can observe that the log returns are centred around 0 on all days, meaning there is no unconditional return bias, though it can be seen that Fridays and Sundays exhibit heavier tails in both directions. It is known that the outliers on Sundays can be attributed to weekend price gaps, as information accumulated over the Saturday trading break is incorporated into prices at the market opening on Sundays. For Fridays, it is likely that institutional participants rebalance or reduce exposure ahead of the weekend, increasing the probability of large price adjustments.

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


*PS: GenAI was used to support the writing of this piece - but mostly for equation writing, cleaning up of markdown formatting, and language!)*
