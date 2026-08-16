# EXP-07 — The harness premium

**2026-08-16 · verdict: refuted · RE-ANALYSIS OF PUBLIC DATA, NOT MY RUN**

That header matters. I did not run this benchmark. I re-analysed the public
[Terminal-Bench 2.1 leaderboard](https://www.tbench.ai/leaderboard/terminal-bench/2.1). It becomes
my experiment the day I run Terminus 2 myself, and not before.

## Hypothesis

A model's own scaffold — Claude Code, Codex, Gemini CLI — beats a model-agnostic reference harness
running the same model. Everyone quotes the top row as though this were settled.

## Method

Every pair on the 2.1 board where the same model appears under both a native scaffold and
**Terminus 2**, the reference harness that exists precisely to hold the model constant. σ is the
delta divided by its combined error bar.

## Result

| Model | Native scaffold | Native | Terminus 2 | Δ | σ | Real? |
|---|---|---|---|---|---|---|
| Gemini 3 Pro | Gemini CLI | 65.8 | 73.9 | **−8.1** | 4.2 | yes, and negative |
| GPT-5.5 | Codex | 83.1 | 78.0 | **+5.1** | 3.1 | yes |
| Fable 5 | Claude Code | 83.8 | 80.4 | +3.4 | 2.0 | marginal |
| Opus 4.7 | Claude Code | 68.9 | 66.1 | +2.8 | 1.4 | no, noise |
| Gemini 3.1 Pro | Gemini CLI | 65.8 | 65.6 | +0.2 | 0.1 | no, noise |

**"The harness premium" does not exist as a general quantity.** It is per-model, and it can be
negative: Gemini's own CLI is 8.1 points **below** a generic harness on the same model and the same
tasks. Two of five pairs are indistinguishable from noise. The row most often quoted, Claude Code
with Fable 5, is the weakest of the three real effects.

## Limits

Single snapshot of a moving leaderboard, read 2026-08-16. Error bars taken as published. No access
to per-task breakdowns, so I cannot say **why** a scaffold loses — only that one does.
