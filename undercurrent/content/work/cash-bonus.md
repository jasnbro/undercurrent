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

Campaign rules from Marketing become versioned campaign terms. Every account then moves through three stages, and it has to pass every check at a stage to reach the next:

- **Eligibility** checks the account when it opens: the promo code, the account and its owner, anti-gaming rules, and whether it opened during the offer period
- **Tracking** checks whether the customer did what their tier asked, such as direct deposits, balance, and statement cycles, inside the tracking window
- **Reward** checks the account again right before paying

Accounts that pass Reward go to the business in a notification, with the rewards to pay attached.

---

## Decisions

**Record why a decision was made.** Storing the result alone would have been simpler, but it wouldn't help someone understand why a customer qualified or didn't. I chose to keep the reasons with the decisions so reviewing an outcome doesn't require reconstructing the logic from scratch.

**Check again right before paying.** Eligibility is decided when an account opens, and a lot can change before payout. The Reward stage reruns the checks that matter at that moment: the account still qualifies, it's in good standing, and the customer hasn't already been paid a bonus of the same type, including from an earlier campaign. An account can be eligible on day one and still be disqualified at payout, and when it is, the reason is recorded. Accounts that were already paid or disqualified aren't picked up again, so a rerun doesn't pay twice.

---

## The risk

An incorrect decision can affect a customer. Reason codes let people review and investigate any outcome, and the checks at payout catch what changed after the account was found eligible. Neither replaces validating the business logic itself.

<!-- TODO(Jasmine): how was it validated before the first real payouts? Parallel run, sample review with Marketing, reconciliation against source? -->

---

## After

- The SQL pipeline is in production and supports customer payouts
- Eligibility and reward outcomes retain their reasons and version history
- Payout re-checks each account, so changes after opening and prior rewards are caught before money moves

---

## What's next

The production implementation defines campaign rules in SQL. I've started exploring a YAML-driven implementation so campaign definitions can be maintained as configuration. That version is not deployed.

<!-- TODO(Jasmine): add "What I'd do differently" in your words. Every other case study has one, and this page shouldn't be the exception. -->

---

I care as much about being able to explain a decision later as I do about getting the calculation right in the first place.
