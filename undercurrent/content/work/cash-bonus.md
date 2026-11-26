# cash bonus

*understanding why a customer qualified*

---

## The problem

A cash bonus campaign needs to answer two questions reliably: who qualifies, and what reward have they earned? I wanted the system to retain enough information to explain those decisions, including when a customer didn't qualify.

<!-- TODO(Jasmine): confirm the "before" picture. Was it one table, built by hand or by a script? Who maintained it? Is there one concrete failure, without bank details, that shows why it had to change? -->

---

## My role

I designed and built the pipeline over about five months, working with Marketing to translate campaign rules into eligibility and reward logic.

<!-- TODO(Jasmine): name anyone you partnered with by role only (e.g. "Marketing's campaign owner"), and say whether anyone else built part of it. -->

---

## The approach

I organized the pipeline into stages and retained their outputs so a reward decision could be traced back through the logic that produced it.

Eligibility and reward decisions are versioned and recorded with reason codes. I wanted the data to explain why a customer didn't qualify as clearly as it explains why another customer did.

<!-- TODO(Jasmine): list the stages in plain words (e.g. qualifying deposits → eligibility → tier → payout), and name the stack (SQL engine, orchestration) where it explains the build. -->

---

## Decisions

**Record why a decision was made.** Storing the result alone would have been simpler, but it wouldn't help someone understand why a customer qualified or didn't. I chose to keep the reasons with the decisions so reviewing an outcome doesn't require reconstructing the logic from scratch.

**Account for reruns in the design.** Pipelines sometimes need to run again after a failure or correction. I used an append-only payout log and a unique constraint to guard against duplicate payout records. That safeguard belongs in the data model rather than depending solely on operating procedures.

---

## The risk

An incorrect decision can affect a customer. Reason codes help people review and investigate outcomes, while the payout log and database constraint address duplication during reruns. Those controls are part of the design, not a substitute for validating the business logic.

<!-- TODO(Jasmine): how was it validated before the first real payouts? Parallel run, sample review with Marketing, reconciliation against source? -->

---

## After

- The SQL pipeline is in production and supports customer payouts
- Eligibility and reward outcomes retain their reasons and version history
- Database-level safeguards address duplicate payout records

---

## What's next

The production implementation defines campaign rules in SQL. I've started exploring a YAML-driven implementation so campaign definitions can be maintained as configuration. That version is not deployed.

<!-- TODO(Jasmine): add "What I'd do differently" in your words. Every other case study has one, and this page shouldn't be the exception. -->

---

I care as much about being able to explain a decision later as I do about getting the calculation right in the first place.
