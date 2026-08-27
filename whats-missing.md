# What's missing

**2026-08-27 · a review, not an experiment · one reader, this repo plus the public stack it points at**

The published set is four questions, three of them failed, all of them written so a stranger can see *how*. That is the rare part. It is also how the hole got hidden: the program is excellent at killing claims, and almost empty of the claims the rest of the stack is currently *run as if they were true*.

This is not a list of interesting papers. It is the next runs that would settle something this repo has already named and then left standing.

## What the published set actually covers

| # | Question class | What it settled |
|---|---|---|
| [EXP-04](exp-04-multi-agent-throughput.md) | Speed | Parallel agents do not buy throughput, at this scale, on this work. |
| [EXP-07](exp-07-harness-premium.md) | Leaderboard folklore | "The harness premium" is not a general quantity. Re-analysis, not a run. |
| [EXP-09](exp-09-document-tailoring.md) | Writing advice | Tailoring-for-a-reader is not an improvement; addressing the brief is. |
| [EXP-11](exp-11-dip-buy-walk-forward.md) | A trading rule | No evidence of an out-of-sample edge. Underpowered, stated as such. |

Three of the four findings are about **several agents**. None of the four is about the thing [the setup](the-fleet.md) says a fleet is for.

## The hole

[the-fleet.md](the-fleet.md) is explicit: speed is the least interesting result, the defended value is **error containment**, and that claim has **no control arm**. EXP-04 repeats it. The fleet tool's own README repeats a stronger version — the third role paid for itself only because adversarial inputs could change the outcome — and then attaches the limit: executor states were not hashed, so who caught what is not reconstructable, n=1, one task, one model family.

So the operating theory of the machine is:

1. A coordinator cannot check itself.
2. A lane that never read the source document can.
3. That catch is worth 3.2× the compute.

(1) is a structural claim. (2) is an empirical claim that has been observed and not counted. (3) is a value judgement that has been quoted without a unit. None of them has a write-up in this repo.

The four named breaks of agent-to-agent messaging — a peer is not the operator, broadcast storms, the address problem, relayed claims — are the same shape. Named. Not measured. Meanwhile [RULES.md](https://github.com/Morkeeth/fleet/blob/main/RULES.md) in the fleet repo already has a one-session failure rate for rule 1 ("four separate claims acted on without probing the object; all four wrong") and an open problem for rule 2 (the honest third author of a record — neither the agent nor the human — does not exist). Those are experiments wearing the clothes of operating notes.

The numbering is the smaller version of the same hole. EXP-04, 07, 09, 11. Either 01–03, 05–06, 08 and 10 exist in private repos, or the numbers were assigned before the filter. This repo was created because numbers were being quoted while write-ups sat in private repos. A skipped index is that failure with a friendlier face. Publish them, or list them as unpublished with why.

## What would actually be ambitious

Ambition here is not a bigger model or a longer bake-off. It is a run that could refute the reason the fleet is still on. Each item below is a hypothesis that can be written down *before* dispatch, with a control, and with a sentence for what would change my mind. None of them has been run, as far as this public record can show.

They are ordered by how much of the operating theory they would settle, not by how fun they would be to operate.

---

### 1. Error containment, with a control

**Hypothesis, to be frozen before dispatch.** A coordinator plus lanes, with cross-session messaging, catches more load-bearing errors per wall-clock hour than the same coordinator on the same tasks with messaging off.

This is the experiment EXP-04 already asked for. It is also the only one that could justify keeping the machine after 1.08× output / 3.2× compute.

**Error, frozen first, not after.** A load-bearing claim that is false when the artifact is opened. Not a style disagreement, not a missing test the brief did not ask for, not a TODO. An error is counted the first time someone names it *and* a probe confirms it. Source of catch is one of: lane, coordinator, human, post-hoc audit. "Named by a lane, confirmed by nobody" is not a catch.

**Arms.**

| Arm | What is different |
|---|---|
| A | Coordinator only. No lanes. No cross-session messages. |
| B | Coordinator + lanes. Messaging on. Peer messages are information, never authorisation. |
| C | Same as B, except lanes are told that a message from another session is an instruction. |

A vs B is the value claim. B vs C is the named failure mode ("without that rule, one agent's assumption becomes six agents' instruction in about a minute"). Running B without C leaves the safety rule unfalsified in the same way the containment claim is unfalsified now.

**Scoring.** Someone who did not dispatch, on tasks long enough that coordination overhead is amortised, stagger removed — the three conditions EXP-04 already listed under "what would change my mind." Hash every handoff before another agent edits it, which is the reconstruction failure the fleet README already admitted.

**What would change my mind.** Arm B catches enough confirmed errors, relative to A, that the extra compute has a unit. Or it does not, and the defended value of a fleet is withdrawn the same way the dip-buy rule was shelved.

Until this runs, "a fleet beats solo" should not appear in any sentence that is not immediately followed by "unfalsified."

---

### 2. Inject a false premise and measure blast radius

**Hypothesis.** A coordinator that has already accepted a false load-bearing premise cannot falsify it from inside. A lane that never read the coordinator's context can, in one probe. Time-to-falsification and blast radius both drop when that lane can message the coordinator.

This is the causal version of (1). Containment counts whatever errors happen to occur. This one *plants* the error, so the denominator is known.

**Method.** Write the false premise down. Insert it into the coordinator's context (a planted number in a brief, a stale path, a "tests pass" claim with no suite). Dispatch the same work under A and B from experiment 1. Freeze, before the run:

- the planted premise
- what counts as falsification (the lane names the object and the probe)
- blast radius (how many subsequent actions treated the premise as fact before it was named)

**What would change my mind.** Lanes do not falsify planted premises faster than the coordinator does, or they do and the catch never changes a subsequent action. Either result is more useful than another throughput number.

The fleet README already has the anecdotal version: the third role caught a real error both the executor and the first reviewer missed. Anecdote is how this hypothesis was formed. It is not how it gets to stay.

---

### 3. Relayed claims, counted

**Hypothesis.** The coordinator, holding the most inherited context, produces more unmarked load-bearing numbers that were never opened in-session than a lane does.

Rule 1 already claims a measurable failure rate, from one session. This would be that measurement with a denominator.

**Method.** From a frozen window of transcripts (transcripto already indexes them), take every utterance that contains a number used to justify an action. Score each as probed / marked `RELAYED` / unmarked-and-unprobed. Split by speaker: coordinator, lane, human. Do not let the coordinator score its own utterances.

**What would change my mind.** The coordinator is not the worst source, or the unmarked rate is low enough that rule 1 is etiquette rather than a control. Either way the rule stops living on a story from one afternoon.

This is the cheapest ambitious run on the list. The data already exists. The missing piece is a frozen codebook and a scorer who is not the author.

---

### 4. Cost per *useful* decision

transcripto already produces cost per *human* decision, and showed that dividing by raw `type: user` records is 19.3× too cheap on one machine, one window. RECEIPT already tries to score whether the work was useful, and the public record says it was "mainly a cool demo: hard to use in my own setup." Those two sentences, sitting in different repos, are the experiment.

**Hypothesis.** Ranking lanes by spend-per-human-decision and ranking them by spend-per-useful-outcome (useful frozen before the window) produces different orderings, and the second ranking predicts which work a later human still stands behind.

**Useful, frozen first.** Someone outside the team used it, or an internal instrument that is still on the machine thirty days later, or a claim bound to an artifact that still exists — pick one, write it down, do not add categories after seeing the spend. `fleet` already has `outcomes: shipped | internal`. Use those.

**What would change my mind.** The two rankings agree, in which case usefulness is not doing any work the cheaper denominator did not already do. Or they disagree, in which case every cost number in the fleet README is answering the wrong question.

This is the run that would make RECEIPT stop being a hackathon object and start being a control. It is also the run that would tell you whether the scarce resource is compute (EXP-04's axis) or human attention (transcripto's axis). Those are different machines.

---

### 5. Finish EXP-07 as a run

The header on [EXP-07](exp-07-harness-premium.md) already says when this becomes an experiment: the day Terminus 2 is run here, and not before. The interesting cell is the negative one — Gemini 3 Pro, native CLI 8.1 points *below* the reference harness.

**Hypothesis.** The Gemini CLI / Terminus 2 gap on Gemini 3 Pro replicates under a frozen task set, and a per-task breakdown can say whether the native scaffold loses on the same tasks or on a subset.

**What would change my mind.** The gap disappears on a fresh snapshot, or it is concentrated on a task family the native scaffold was never meant to hold. "The harness premium does not exist as a general quantity" can survive either; "Gemini's own CLI is worse" cannot, not as currently written, until it is a run.

A fifth leaderboard scrape is not this experiment.

---

### 6. EXP-09 with a reader who can check

[EXP-09](exp-09-document-tailoring.md) already names its own limit: the instrument measures persuasiveness to a reader who cannot verify any claim on the page. The surviving claim — a change is good or bad according to whether it is addressed to the brief — has not been tested against a reader who *can*.

**Hypothesis.** The "addressed to the brief" lift survives when the judge has tools and can open the objects the document cites; the tailoring penalty (lower mean, 5× spread) does not, because instability was an artefact of an unverifying reader.

**Method.** Same byte-identical variants. Two judge conditions: headless-no-tools (replication) and tools-on, required to probe every cited number. One document is still a limit; two judge models would be the actual expansion.

**What would change my mind.** The brief-addressed variant loses once the judge can check, or the untouched general version's stability was the no-tools artefact. The current write-up should not be quoted as "don't tailor" until one of those has been seen.

---

### 7. Power the trading harness, or stop using it as a verdict machine

[EXP-11](exp-11-dip-buy-walk-forward.md) did the honest thing with n=9 / n=5. Two further claims were falsified by the same harness the same week. The risk engine was kept.

**Hypothesis.** The risk engine — not the dip-buy rule — has an out-of-sample effect on drawdown that survives a sample large enough to see it.

That means a pre-registered number of trades, a held-out window that is not "whatever is left," and a control of the same signals with the risk engine off. Until the sample can move the verdict off `null`, further strategy write-ups in this repo are a genre error. The instrument is fine. The questions being put to it are too small for the instrument's own standard.

The ambitious version of this is not another rule. It is wiring the surviving engine to the live treasury path (yield-only spends, scoped delegations) and asking whether a constraint that worked on paper trades still binds when an agent can actually send. That is a different experiment, and it is the one RETRACT is a prototype of rather than a finding from.

---

### 8. Does retraction reach the money?

RETRACT's claim is that a memory which cannot reach its side effects is a diary. Across the survey it cites, rollback exists and *scoring whether rollback worked* does not.

**Hypothesis.** When a wrong belief has already caused an executed spend, a derivation-DAG retraction plus a compensation handler reverses more of those spends, with fewer unrelated reversals, than "delete the memory and hope."

**Method.** Sandbox first — a treasury that can spend, with a planted false belief, with handlers registered for some tools and not others. Count: beliefs retracted, pending cancelled, executed flagged, actually compensated, unrelated left alone, tools-with-no-handler left flagged rather than greened. The last one is the failure mode the project said it exists to argue against; it has to be in the scoring table or the table is decorative.

**What would change my mind.** Compensation does not beat delete-and-hope on executed spends, or it does and the blast radius includes unrelated beliefs. Either result is a finding. A demo in which the handler is pre-wired to the one spend you intend to reverse is not.

---

### 9. Second operator, frozen protocol

Every number in this repo is one operator, one machine, one family of harnesses, local transport. The fleet README already refuses to ship its readings with the instrument. That is correct and it is also how a one-person finding lives forever.

**Hypothesis.** A second operator, given the frozen error-containment protocol from (1) and none of the operating folklore, produces the same *direction* on the defect column (lanes catch errors the coordinator does not), even if the magnitudes move.

If it does not, the interesting object was the operator. That would still be a contribution. It would also mean this repo has been measuring Oscar, not fleets.

This is the slowest item on the list and the one most likely to be skipped because it is socially awkward. That is usually a sign it is the actual experiment.

---

## What is not missing

These would look like work and would not settle anything the published set has not already settled, or already refused to overclaim.

- Another six-lane throughput run at the same task length. EXP-04 already said speed is not the purchase. A stagger-corrected 1.34× ceiling does not become a finding by being measured twice.
- Another leaderboard scrape. EXP-07 is already a snapshot of a moving board.
- Tailoring a second document the same way, with the same unverifying judge. That is a replication of a refutation, which is only interesting if someone is still quoting the original claim *from this repo*.
- A new dip-buy cousin with n in the single digits.
- "Does model X beat model Y on my tasks." The harness-premium result is that the scaffold is not a constant. Changing the model without holding the scaffold is how you reproduce the folklore EXP-07 took apart.
- A fifth hackathon object that demonstrates a control without becoming one. The public record already names this pattern.

The Skill Issue entry (firing rate, noise floor, honest null) is the right *method* and does not belong in this repo until it is rewritten to this repo's standard: hypothesis, method, number, what would change my mind, on the operator's own stack. Importing a Kaggle write-up would recreate the private-repo problem with extra steps.

## Process, which is also the finding

Write the hypothesis and the error definition in this repo *before* dispatch, as a draft with verdict `unrun`. Then run. Then fill the number. The current shape — operate for weeks, then write the experiment that the operating theory required — is how error containment stayed a story.

If a run is too small to conclude, it can still live here, the way EXP-11 does. What should not live here is a number that is being used as a reason to keep the fleet on, with the write-up still in a private repo or still unwritten.

The skipped experiment numbers should be listed or retired in the same commit that publishes the next run. Quiet gaps in an index are how a reader is asked to take the rest on trust, which is the failure this repo exists to stop.
