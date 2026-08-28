# experiments

Four experiments on my own agent stack, 2026. Three of them failed.

They are here because the results were being quoted on a portfolio while the write-ups sat in
private repos, which meant a reader was asked to take four numbers on trust. That is the failure
these experiments are mostly about, so leaving it in place was not an option.

| # | Question | Verdict |
|---|---|---|
| [EXP-04](exp-04-multi-agent-throughput.md) | Does running six agents in parallel produce more than running one? | **null** |
| [EXP-07](exp-07-harness-premium.md) | Does a model's native scaffold beat a generic harness? | **refuted** (re-analysis, not my run) |
| [EXP-09](exp-09-document-tailoring.md) | Does tailoring a document to its reader improve it? | **refuted** |
| [EXP-11](exp-11-dip-buy-walk-forward.md) | Does the dip-buy rule have an out-of-sample edge? | **null** |
| [EXP-12](exp-12-relayed-claims.md) | Does the coordinator pass unmarked numbers it never opened? | **unrun** |
| [EXP-13](exp-13-planted-premise.md) | Does a lane falsify a planted coordinator premise? | **unrun** |
| [EXP-14](exp-14-error-flow.md) | Do errors flow down from lanes or up from the coordinator? | **unrun** |
| [EXP-15](exp-15-delivery-is-not-success.md) | Does `send_message` success mean the recipient got it? | **unrun** |
| [EXP-16](exp-16-verify-at-handoff.md) | Does probing at the peer-message boundary cut planted-claim survival? | **unrun** |
| [EXP-17](exp-17-sequential-penalty.md) | Is EXP-04's null the sequential penalty on coding work? | **unrun** |

Skipped numbers: [01, 02, 03, 05, 06, 08, 10](unpublished.md) — fill or retire. 14–17 were
assigned anyway because the next runs are lanes, not a fifth throughput number.

**Dispatch from [lanes.md](lanes.md).** 15 before 13 and 16. 14 and 17 share a task panel.

**Start with [the setup](the-fleet.md)** — what a fleet is, the in-session messaging feature it is
built on, what agent-to-agent communication made possible, and the four ways it breaks. Three of the
four findings below are about behaviour that only exists when there are several agents.

**Then [what's missing](whats-missing.md)** — the operating theory this repo has named and not
measured, and the next runs that would settle it. A review, not an experiment.

**Dispatch from [lanes.md](lanes.md)** — one outcome per terminal. 15 before 13 and 16.

**Maintainer:** Oscar Mörke. Findings are reproducible from the write-ups; corrections welcome as
issues.

Each write-up states the hypothesis before the method, the method before the number, and what
would have changed my mind. Where a sample is too small to conclude, it says so instead of
rounding up to a finding.
