# Lanes

Each row is one outcome. Dispatch one terminal per row. Do not let the coordinator
score its own lane.

12 and 13 are the cheap pair from the earlier cut. 14–17 are the ambitious set: they
need a fleet, a frozen task panel, or a lying transport, and they are aimed at cells
the 2026 literature left open rather than at another throughput number.

| Lane | File | Outcome | Needs | Verdict |
|---|---|---|---|---|
| relay | [EXP-12](exp-12-relayed-claims.md) | unmarked-number rates by speaker | existing transcripts | unrun |
| plant | [EXP-13](exp-13-planted-premise.md) | two rows, one lie, n=1 | two terminals | unrun |
| flow | [EXP-14](exp-14-error-flow.md) | upward catch vs downward amplification on the same traces | task panel, solo vs fleet, independent scorer | unrun |
| wire | [EXP-15](exp-15-delivery-is-not-success.md) | success-ack vs enqueue, with payload hashes | send_message + recipient transcripts | unrun |
| gate | [EXP-16](exp-16-verify-at-handoff.md) | planted-claim survival at handoff vs at the end | messaging on, three verify conditions | unrun |
| split | [EXP-17](exp-17-sequential-penalty.md) | solo vs fleet split by sequential / decomposable, labelled first | task panel labelled before dispatch | unrun |

**Order.** 15 before 13 and 16: if the wire does not deliver, those two are measuring a
machine that is not there. 14 and 17 share a task panel; label it once, run both, do not
relabel after seeing scores.

**Do not dispatch.** Another six-lane throughput bake-off. Another leaderboard scrape.
Terminus 2 as a substitute for 14. Growing 13 into 14 after seeing 13's two rows.
