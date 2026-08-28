# EXP-15 — Delivery is not success

**unrun · hypothesis and probes frozen before the sends · my own run**

The fleet is built on Claude Code in-session messaging: one session sends, the other
receives a `<cross-session-message>` mid-turn without stopping. [the-fleet.md](the-fleet.md)
treats that as the feature that turns six terminals into a system.

In August 2026 the transport was observed lying. `send_message` returns a success
acknowledgement when nothing was enqueued: no `queue-operation`/`enqueue` on the
recipient, no new transcript record, sometimes a wedge (`hadFirstResponse=false`) for
15–20 minutes. Documented on the harness's own tracker, among others
[#86012](https://github.com/anthropics/claude-code/issues/86012),
[#86603](https://github.com/anthropics/claude-code/issues/86603),
[#87286](https://github.com/anthropics/claude-code/issues/87286),
[#88125](https://github.com/anthropics/claude-code/issues/88125),
[#88777](https://github.com/anthropics/claude-code/issues/88777). One report: 197
consecutive success acks, zero deliveries. Another: a send to a session name that has
never existed, still `success: true`. Another: silent truncation (~6.7KB sent, ~4.7KB
delivered) with no flag.

If delivery is not success, every experiment that assumes a lane heard the coordinator
is uninterpretable. Run this before EXP-13 and EXP-16.

## Hypothesis, written before the sends

A non-empty fraction of `send_message` calls that return success do not appear as an
enqueue in the recipient's transcript, on this machine, this build, this week.

The address problem in the-fleet.md (handles are socket-derived, a restart gets a new
handle, the coordinator's map goes stale silently) is a special case: the send can
succeed at a name that is no longer that lane.

## Build, frozen before the sends

- Claude Code / Desktop / CCD version:
- OS:
- window (UTC):
- n planned sends:

If the version line is blank, this file is a draft.

## Probe, frozen first

Each send carries a unique payload whose sha256[:16] is written down **before** the
call, not after reading the recipient.

For each send, score from the **recipient's** disk, not from the sender's tool result
and not from the UI card:

| Probe | Pass |
|---|---|
| sender result | string contains success / "Message sent" |
| enqueue | a `queue-operation` with `enqueue` (or the current equivalent) contains the payload hash |
| transcript | the recipient `.jsonl` gains a record containing the payload hash |
| agent-visible | asking the recipient "what was the last peer message hash?" returns that hash |
| truncation | received length equals sent length; if not, record both |
| wedge | recipient produces a first token within 120s of enqueue; if it sits in
`hadFirstResponse=false`, that is a wedge even if the card rendered |

A UI card without an enqueue is a **false delivery**. A success string without an
enqueue is a **lying ack**. Those are different rows.

Include, as labelled conditions, not as accidents:

1. recipient idle
2. recipient mid-turn
3. send to a handle that has been restarted since the coordinator's map was written
4. send to a name that has never existed
5. payload above 5KB and below 8KB (truncation check)

n ≥ 20 across those five, with the planned counts written here before the first send:

- idle:
- mid-turn:
- stale handle:
- never-existed:
- oversized:

## Result

| Condition | n | lying ack | false delivery | enqueued | agent-visible | truncated | wedged |
|---|---|---|---|---|---|---|---|
| idle |  |  |  |  |  |  |  |
| mid-turn |  |  |  |  |  |  |  |
| stale handle |  |  |  |  |  |  |  |
| never-existed |  |  |  |  |  |  |  |
| oversized |  |  |  |  |  |  |  |

**Delivery rate** = enqueued / (sends that returned success). Write it. If it is 1.0
on this build, say so; the GitHub threads are then someone else's machine.

## What this does and does not show

It shows whether the wire this fleet is built on reports the physical fact of delivery.
It does not show that messaging is worthless when it does deliver. It does not fix the
harness.

If delivery rate is 0, EXP-13 and EXP-16 cannot run on this build. Write that on those
files rather than running them anyway.

## What would change my mind

Every success ack in the window has a matching enqueue and an agent-visible hash, including
stale and never-existed names (those two should *error*, not deliver). That would mean
the August 2026 failure is not on this machine, and the address problem is still a
map problem rather than a lying-ack problem.
