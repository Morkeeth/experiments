# EXP-04 — Multi-agent throughput

**2026-08-14 · verdict: null · my own run**

## Hypothesis, written before the run

Running six coding agents in parallel produces meaningfully more finished work per hour than
running one. I had been operating as though this were true for weeks.

## Method

Six lanes dispatched against one solo baseline on comparable tasks. Output counted as work
produced; cost counted as the sum of per-lane durations, because six agents running for ten
minutes costs six times ten minutes of compute regardless of the wall clock.

**A bias I introduced and declared before seeing results:** lanes 4 to 6 and the solo control were
dispatched about 2.2 minutes after lanes 1 to 3, because I stopped to read a message. That inflates
the fleet's measured wall clock, so a stagger-corrected ceiling is printed beside the measured
figure rather than instead of it.

## Result

**1.08× the output for 3.2× the compute.** 955 agent-seconds against the solo baseline's 297.
Correcting for the dispatch stagger — best case, all six launched in one breath — the ceiling is
**1.34×**.

## What this does and does not show

It does not show that parallel agents are useless. It shows that **speed is not what they buy**, at
this scale, on this work, with this operator. The value I can defend is error containment: a lane
that has not read the coordinator's context catches errors the coordinator cannot catch in itself.

**No control arm was run for the error-containment claim.** So "a fleet beats solo" is unfalsified
rather than proven, and I am not going to write it as though it were proven.

## What would change my mind

A run where output is scored by someone who did not dispatch it, on tasks long enough that
coordination overhead is amortised, with the stagger removed.
