# The setup: a fleet, and why agent-to-agent messaging changed it

Every experiment in this repo was run on the same machine, and the machine is worth describing
before the results, because three of the four findings are about **how agents behave when there
are several of them** rather than about any single model.

## What a fleet is here

Several Claude Code terminals working in parallel on one operator's projects. One is the
**coordinator**; the rest are **lanes**. A lane owns one repo, one branch, and one outcome. The
coordinator holds context, dispatches, and — this is the part that matters — **is the single point
that cannot check itself.**

## The feature it is built on

Claude Code shipped **in-session messaging**: one running session can send a message to another,
and the receiving session gets it wrapped as a `<cross-session-message>` mid-turn, without either
one stopping. Before that, parallel agents were parallel *monologues* — you could run six terminals
but they could not tell each other anything, so every correction had to route through the human at
the centre.

Agent-to-agent messaging is what turns six terminals into a system. It also creates the failure
modes below, which is the honest half.

## What it made possible, and what it broke

**Possible: a lane can block the coordinator.** The most valuable message this system produces is a
lane saying *"you aimed me at the wrong object."* A coordinator that has already accepted a false
premise cannot falsify it from the inside; a lane that never read the source document can, in one
probe. Several of the findings in this repo exist because that message got sent.

**Broken, and worth naming:**

- **A peer is not the operator.** A message from another agent is information, never authorisation.
  Without that rule, one agent's assumption becomes six agents' instruction in about a minute.
- **Broadcast storms.** Any agent able to message every peer will, and the message board floods
  until lanes lose track of which one they are.
- **The address problem.** Session handles are socket-derived and carry no lane identity, so the
  coordinator's map of handle → lane exists only inside the coordinator. A terminal that dies and
  restarts gets a new handle and the map goes stale silently.
- **Relayed claims.** The coordinator holds the most inherited context and therefore the most
  second-hand numbers. It is structurally the position most likely to pass on a figure it never
  opened.

## Why the throughput result is the least interesting one

[EXP-04](exp-04-multi-agent-throughput.md) says a fleet produced 1.08× the output for 3.2× the
compute. That is a real measurement and it is not the reason to run one.

What a fleet buys, as far as this setup can show, is **error containment** — and that claim has no
control arm, so it is stated as unproven rather than dressed as a finding. The measurement that
would settle it is a count of errors caught by a lane versus by the coordinator, over a defined
window, with the definition of "error" written down **before** the run rather than after. That
number has been quoted at four different values inside one day by people who never agreed on the
unit, which is exactly why it is not quoted here.

The next runs that would actually settle that claim — and the other named-but-unmeasured parts of
this setup — are in [what's missing](whats-missing.md). Dispatch them as lanes from
[lanes.md](lanes.md). The 2026 literature measured error amplification *downward* (worker to
output). This setup's claim is the other direction. That is [EXP-14](exp-14-error-flow.md). The
wire the claim runs on currently reports success without enqueueing; that is
[EXP-15](exp-15-delivery-is-not-success.md), and it goes first.

## Reproducing any of this

The tool and its findings are public at [github.com/Morkeeth/fleet](https://github.com/Morkeeth/fleet).
The write-ups in this repo state the hypothesis before the method and the method before the number.
Where a sample is too small to conclude, they say so.
