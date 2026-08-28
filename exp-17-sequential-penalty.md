# EXP-17 — Sequential penalty, on this work

**unrun · hypothesis and labels frozen before dispatch · my own run**

Kim, Liu et al. ([arXiv:2512.08296](https://arxiv.org/abs/2512.08296)): centralized
multi-agent coordination improved parallelizable financial reasoning by 80.9% over a
single agent, and **every** multi-agent variant they tested **degraded** sequential
reasoning (PlanCraft) by 39–70%. Coordination yields diminishing or negative returns
once a single-agent baseline is already past ~45% (ˆ = −0.408). Tool-heavy tasks tax
multi-agent overhead harder.

This fleet's everyday work is coding: long-horizon, tool-dense, mostly sequential.
Solo on the fleet README's one task scored 91. EXP-04 measured 1.08× output for 3.2×
compute on "comparable tasks" that were not labelled sequential vs decomposable
before the run.

**Hypothesis: EXP-04's null is the sequential penalty, not a general fact about
fleets.** If the panel is split first, the fleet should beat solo on the decomposable
slice and lose on the sequential slice. If it loses on both, EXP-04 was the finding
and the architecture-task story does not save it.

## Hypothesis, written before dispatch

On tasks labelled decomposable before dispatch, fleet wall-clock output per human
hour exceeds solo. On tasks labelled sequential before dispatch, it does not, and
compute-adjusted output is worse.

Do not relabel a task after seeing which arm won.

## Labels, frozen first

**Sequential.** Later steps need the artifact of earlier steps. Two agents on it will
wait or collide. Examples: a failing test whose fix changes the next failure; a
migration; a bisect.

**Decomposable.** Subtasks can be finished without reading each other's working trees.
Examples: three independent bugs in three files; docs in one repo and tests in
another; a review of a frozen diff.

Write at least four of each, here, before dispatch. Shared with [EXP-14](exp-14-error-flow.md)
if both run in the same window.

| id | brief | sequential or decomposable | why (one line) |
|---|---|---|---|
|  |  |  |  |

A task you cannot label is not on the panel.

## Arms

| Arm | Setup |
|---|---|
| S | Solo. |
| F | Coordinator + lanes, messaging on, peer messages are not authorisation. |

Same scoring as EXP-04 for output (finished work against the brief) and cost (sum of
per-lane durations, not wall clock). Stagger removed or declared before launch.
Independent scorer who did not dispatch. Hash F handoffs.

Also record, because Kim's second finding is a ceiling: the solo scorer's 0–100 on
each task. If solo is already high, the decomposable slice may still fail to pay.

## Result

| Slice | n | solo output | fleet output | fleet/solo output | fleet/solo compute | mean solo score |
|---|---|---|---|---|---|---|
| sequential |  |  |  |  |  |  |
| decomposable |  |  |  |  |  |  |

Verdict stays `unrun` until both slices have n ≥ 4. Pooling them into one ratio is
how EXP-04 hid this, if it is here.

## What this does and does not show

It shows whether this operator's work is in the regime where centralized MAS is
supposed to help, the regime where it is supposed to hurt, or both. It does not
overturn Kim et al.; it asks whether this fleet was being run on the wrong slice
and calling that "fleets don't buy speed."

If both slices are null or negative, the sequential-penalty explanation is
withdrawn and EXP-04 stands.

## What would change my mind

The decomposable slice does not beat solo on output, or it does and the sequential
slice also does (the split was decorative). Either way the operating rule in the
fleet README — "solo for bounded implementation, full fleet when adversarial
judgement can change the answer" — has to be rewritten against this table, not
against one unlabelled bake-off.
