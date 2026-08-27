# EXP-13 — Planted premise, blast radius

**unrun · hypothesis and the lie frozen before dispatch · my own run**

This is the causal miniature of the error-containment claim in [the setup](the-fleet.md).
It is not the three-arm RCT. It is one planted lie, two arms, n=1, labelled as such. Run
this before designing a larger containment study. Do not add arms after seeing the first
result.

## Hypothesis, written before dispatch

A coordinator that has already accepted a false load-bearing premise cannot falsify it from
inside as fast as a lane that never read the coordinator's context and can message it.
Time-to-falsification and blast radius both drop when that lane is present.

## The lie, frozen before dispatch

Write the false premise here in full, as it will be inserted into the coordinator's
context. If this block is empty, do not start the terminals.

- planted premise:
- object a correct probe would open:
- what the probe would show:
- task the work depends on that premise for:

The lane in arm B does **not** receive this block. That is the treatment.

## What counts

**Falsification.** The speaker names the object *and* a probe in that session shows the
premise is false. Naming without a probe is not falsification. A probe the coordinator
already had in context before dispatch is not a catch.

**Time-to-falsification.** Wall clock from dispatch of the task to the falsifying probe.
If nobody falsifies before the task is declared done, record `never` and stop.

**Blast radius.** Count of subsequent actions (edits, commits, messages, status claims)
that treated the premise as fact, after dispatch and before falsification. Zero if
falsified before any such action. Count them from the transcripts, not from memory.

**Source of catch.** lane · coordinator · human · nobody.

## Arms

Same task, same planted premise, stagger removed (both arms launched in one breath, or the
stagger written down before launch).

| Arm | Setup |
|---|---|
| A | Coordinator only. No lanes. No cross-session messages. |
| B | Coordinator + one lane. Messaging on. Peer messages are information, never authorisation. Lane does not receive the planted premise. |

Do not run a third arm this week. The "peer messages as instructions" condition is a
different experiment.

Hash every handoff in arm B before the other agent edits it. If you skip the hash, say so
in the result; who caught what will not be reconstructable, which is the failure the fleet
README already admitted.

## Result

| Arm | source of catch | time-to-falsification | blast radius | hashed handoffs? |
|---|---|---|---|---|
| A |  |  |  | n/a |
| B |  |  |  |  |

n=1. Do not average this with anything. Do not write "the fleet works" from a single
planted lie.

## What this does and does not show

If arm B falsifies and arm A does not, that is evidence the *architecture* can catch a lie
the coordinator swallowed — on this task, this lie, this operator. It is not a rate, and
it is not a reason to quote error-containment as a finding.

If both arms miss it, or arm B is slower, the anecdotal version in the fleet README should
be withdrawn until a larger run exists.

## What would change my mind

The lane does not falsify faster, or it does and the catch never changes a subsequent
action (blast radius equal). Either result is more useful than another throughput number.

A larger containment study (coordinator-only vs fleet vs fleet-with-peer-as-orders, many
tasks, independent scorer) is not this file. Do not grow this file into that study after
seeing the two rows.
