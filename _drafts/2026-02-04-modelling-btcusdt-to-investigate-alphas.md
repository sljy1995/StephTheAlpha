---
layout: post
title: "Modelling BTCUSDT to Investigate Alphas - Part I: Analysis of BTCUSDT"
date: 2026-02-04
excerpt: ""
---
__All content here is for research and educational purposes only, not financial advice.__

# Introduction

## Why is BTCUSDT Worth Studying?
Cryptocurrency, because of its 24/7 continuous trading nature, presents different volatility clustering and gap dynamics. Within the cryptocurrency universe of traded pairs, BTCUSDT is the most traded, and serves as a natural benchmark to be studied. The accessibility of crypto perpetuals (perps) to retail traders provides leverage and the option to monetise convexity. Funding rates also presents as another form of risk premium that could be capitalised. These make BTCUSDT an ideal setting to study volatility, derivatives, and market microstructure. 

## Statistical Analysis of BTCUSDT

I studied per-minute aggregated spot trades of BTCUSDT aggregated using the dataset of BTCUSDT microseconds spot trades from 2017-08-17 to 2025-08-01 (~ 8 years worth of data). Log returns were also derived 
