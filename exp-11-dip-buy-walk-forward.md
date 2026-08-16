# EXP-11 — Dip-buy rule, walk-forward

**2026-08-09 · verdict: null · my own run**

## Hypothesis

A dip-buy rule I had been running has an edge that survives out of sample.

## Method

Walk-forward. Train 2024-05 to 2025-12, held out 2026-01 to 2026-08. No parameter refitting on the
held-out window.

## Result

| | train | held out |
|---|---|---|
| net % of margin | +47.6% | +2.0% |
| win rate | 67% | 40% |
| median trade | +24.6% | **−50.3%** |
| n | 9 | 5 |

The edge collapses out of sample and the median held-out trade loses half its margin.

## What this does not show

**n=9 and n=5 is underpowered and I am not going to pretend otherwise.** This does not prove the
strategy is dead. It shows there is **no evidence it is alive**, which is a different and weaker
statement, and it is the one the data supports.

## What I did about it

Shelved the strategy, kept the risk engine. Two further claims I made the same week were falsified
by the same harness and withdrawn: a trailing ratchet that turned +31.3% of margin into +0.3% by
exiting winners at the locked floor, and a funding-carry idea that needed roughly 0.11% per hour to
clear fees when the richest available carry was 0.00125%.
