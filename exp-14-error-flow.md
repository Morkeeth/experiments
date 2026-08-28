# EXP-14 — Error flow, both directions

**unrun · hypothesis and task panel frozen before dispatch · my own run**

Kim, Liu et al., *Towards a Science of Scaling Agent Systems*
([arXiv:2512.08296](https://arxiv.org/abs/2512.08296), Google Research blog 2026-01-28):
error amplification is **downward**. A worker mistake reaches the final result.
Independent multi-agent systems amplify failures 17.2× relative to a single-agent
baseline; a centralized orchestrator contains that to 4.4× by acting as a validation
bottleneck. Their unit is relative task-failure probability, MAS/SAS, not a count of
catches.

This fleet's operating theory is the **other direction**. A coordinator that has
accepted a false premise cannot falsify it from inside; a lane that never read the
source document can. [the-fleet.md](the-fleet.md) and [EXP-04](exp-04-multi-agent-throughput.md)
name that as error containment and mark it unproven. The literature does not measure it.
The orchestrator, in Kim's topology, is the filter. Here it is the suspected source.

[EXP-13](exp-13-planted-premise.md) is the n=1 miniature. This file is the panel.

## Hypothesis, written before dispatch

On the same traces, a centralized fleet (coordinator + lanes, messaging on) will show:

1. **Downward** (Kim's direction): fewer lane-originated defects in the shipped artifact
   than a no-messaging control, because the coordinator can act as a bottleneck.
2. **Upward** (this fleet's direction): more coordinator-originated defects caught by a
   lane than by the coordinator itself.

If (2) is false, the operating theory is withdrawn. If (1) is false and (2) is true, the
fleet is a detector pointed at its own centre, not a worker-validator of the Google
shape, and should not be described as "centralized containment." If both are false, the
machine is 3.2× compute for a story.

Do not import 17.2× or 4.4× into the result table. Different unit, different tasks,
different models. The comparable object is the *direction*, scored on this panel.

## Task panel, frozen before dispatch

At least eight tasks. Each labelled **before seeing any output** as sequential or
decomposable — the same split [EXP-17](exp-17-sequential-penalty.md) uses. Write the list
here. If the list is empty, this file is a draft.

- panel (id, one-line brief, sequential|decomposable):
- independent scorer (did not dispatch):
- model family:
- window:

A task the coordinator has already been briefed on for weeks is not on the panel.

## Error, frozen first

A load-bearing claim that is false when the artifact is opened. Not style, not an
unrequested test, not a TODO.

**Origin.** coordinator · lane · solo · unknown. Origin is the session that first
wrote the false claim, reconstructed from hashed handoffs. If handoffs were not hashed,
origin is `unknown` and that task does not enter the direction table.

**Fate.** caught-by-lane · caught-by-coordinator · caught-by-human · caught-at-audit ·
shipped. "Caught" means named *and* probed in that session, same rule as EXP-13.

**Downward amplification, Kim's unit, on this panel only.** Task-failure rate of the
fleet arm divided by task-failure rate of the solo arm. Failure means the independent
scorer rejects the artifact against the brief written before dispatch. Report the ratio
and both rates. Do not call it 4.4× unless the number is 4.4.

## Arms

| Arm | Topology |
|---|---|
| S | Solo. No lanes. No cross-session messages. |
| F | Coordinator + lanes. Messaging on. Peer messages are information, never authorisation. |

Same tasks, stagger removed or written down before launch. Hash every F handoff before
the other agent edits it. Run [EXP-15](exp-15-delivery-is-not-success.md) on the same
window; a message that never enqueued is not a handoff.

Do not add the peer-as-instruction arm here. That is a different hypothesis.

## Result

**Direction table** (errors with known origin):

| Origin | n | shipped | caught-by-lane | caught-by-coordinator | caught-by-human | audit |
|---|---|---|---|---|---|---|
| coordinator |  |  |  |  |  |  |
| lane |  |  |  |  |  |  |
| solo |  |  |  |  |  |  |

**Kim unit, this panel:**

| Arm | tasks | failures | failure rate | MAS/SAS |
|---|---|---|---|---|
| S |  |  |  | 1.0 |
| F |  |  |  |  |

Verdict stays `unrun` until both tables have numbers. n=1 from EXP-13 does not get copied
in.

## What this does and does not show

It shows whether this fleet contains errors the way a centralized MAS is supposed to,
whether it contains errors the way this repo claims, both, or neither — on this panel,
this operator, this model family. It does not show that "more agents help." EXP-04
already refused that.

## What would change my mind

Upward catch is no better than coordinator self-catch. Or downward amplification is
worse than solo and upward catch does not pay for it. Either result shelves the
defended value the same way the dip-buy rule was shelved.
