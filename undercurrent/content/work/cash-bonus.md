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

Campaign rules from Marketing become versioned campaign terms. From there, three stages run in order: eligibility decides who qualifies, tier tracking follows each customer's activity to the tier they reach, and rewards decides who gets paid. Downstream, the rewards drive customer notifications and the export the business uses to pay.

---

## Decisions

**Record why a decision was made.** Storing the result alone would have been simpler, but it wouldn't help someone understand why a customer qualified or didn't. I chose to keep the reasons with the decisions so reviewing an outcome doesn't require reconstructing the logic from scratch.

**Check prior rewards before paying.** Pipelines get rerun after a failure or a correction. Before anyone is paid, the rewards stage checks whether that customer was already rewarded. If they were, they're marked disqualified with a reason code instead of being paid again, so a would-be duplicate shows up in the data as an explained no.

---

## The risk

An incorrect decision can affect a customer. Reason codes let people review and investigate any outcome, and the prior-reward check keeps a rerun from paying someone twice. Neither replaces validating the business logic itself.

<!-- TODO(Jasmine): how was it validated before the first real payouts? Parallel run, sample review with Marketing, reconciliation against source? -->

---

## After

- The SQL pipeline is in production and supports customer payouts
- Eligibility and reward outcomes retain their reasons and version history
- Customers who were already rewarded are disqualified with a reason code, not paid again

---

## What's next

The production implementation defines campaign rules in SQL. I've started exploring a YAML-driven implementation so campaign definitions can be maintained as configuration. That version is not deployed.

<!-- TODO(Jasmine): add "What I'd do differently" in your words. Every other case study has one, and this page shouldn't be the exception. -->

---

I care as much about being able to explain a decision later as I do about getting the calculation right in the first place.
