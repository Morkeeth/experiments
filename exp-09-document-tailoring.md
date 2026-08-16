# EXP-09 — Does tailoring a document to its reader improve it?

**2026-08-16 · verdict: refuted · my own run**

## Hypothesis

A document rewritten for one specific reader beats the untouched general version with that reader.
This is close to universal advice.

## Method

A blind panel of six judges, run headless with no memory, no tools and no context about the author,
scores a document against a target brief. Three repeats per variant, **eighteen judges per data
point**. Critically: **everything outside one sentence was byte-identical between variants**, so the
only moving part was the sentence under test.

## Result

| Variant | mean | runs | spread |
|---|---|---|---|
| untouched general version | **7.6** | 7.5 / 7.7 / 7.5 | **0.17** |
| full rebuild for the target | 7.4 | 6.8 / 7.7 / 7.7 | 0.83 |
| minimal targeted patch | 7.0 | 7.3 / 6.7 / 7.0 | 0.67 |

The tailored versions scored lower **and were five times less stable**. The spread is the finding:
the untouched document lands on the same number three times running; the tailored one swings.

**Replicated.** An independent run three days earlier produced the same two spreads to two decimal
places — 0.83 tailored against 0.17 untouched.

## The correction that came out of it

A later variant, changed by one sentence in the other direction, scored **7.8** — the highest
measured. The difference was not tailoring versus not tailoring. It was **whether the change was
addressed to something the target actually asked for.** The same edit was worth +0.14 on a brief
that named the requirement and −0.6 on one that did not.

So the refuted claim is "tailoring helps." The surviving claim is narrower and more useful:
**a change is not good or bad, it is addressed to the brief or it is not.**

## Limits

One document, one family of briefs, one judge model. The instrument measures persuasiveness to a
reader who cannot verify any claim on the page, which is a real property of real readers but not
the only one.
