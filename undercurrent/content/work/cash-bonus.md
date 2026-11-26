# cash bonus

*a reason behind every reward decision*

---

## The problem

A cash bonus campaign needs to answer two questions reliably: who qualifies, and what reward have they earned? I wanted the system to retain enough information to explain those decisions, including when a customer didn't qualify.

Before this, a single table and a single process handled eligibility, rewards, and payment notification together, with no granular reason codes. The data could show what happened to an account, but not why.

---

## My role

I designed and built the pipeline over about five months, working with the director of operations and operations line-of-business managers to translate campaign rules into eligibility, tracking, and reward logic.

---

## The approach

I organized the pipeline into stages and retained their outputs so a reward decision could be traced back through the logic that produced it.

Eligibility and reward decisions are versioned and recorded with reason codes. I wanted the data to explain why a customer didn't qualify as clearly as it explains why another customer did.

Campaign rules from Marketing become versioned campaign terms. Every account then moves through three stages, and it has to pass every check at a stage to reach the next:

- **Eligibility** checks the account when it opens: the promo code, the account and its owner, anti-gaming rules, and whether it opened during the offer period
- **Tracking** checks whether the customer did what their tier asked, such as direct deposits, balance, and statement cycles, inside the tracking window
- **Reward** checks the account again right before payout

Accounts that pass Reward go to the business in a notification, with the rewards to pay attached.

---

## Decisions

**Record why a decision was made.** Storing the result alone would have been simpler, but it wouldn't help someone understand why a customer qualified or didn't. I chose to keep the reasons with the decisions so reviewing an outcome doesn't require reconstructing the logic from scratch.

**Check again right before payout.** Eligibility is decided when an account opens, and a lot can change before payout. The Reward stage reruns the checks that matter at that moment: the account still qualifies, it's in good standing, and the customer hasn't already been paid a bonus of the same type, including from an earlier campaign. An account can be eligible on day one and still be disqualified at payout, and when it is, the reason is recorded. Accounts that were already paid or disqualified aren't picked up again on a rerun. The pipeline decides who is ready to be paid; the business makes the payment.

---

## The risk

An incorrect decision can affect a customer. Reason codes let people review and investigate any outcome, and the checks at payout catch what changed after the account was found eligible. Neither replaces validating the business logic itself. Before the first payouts, I tested the business logic and the system with test data.

---

## After

- The SQL pipeline is in production and supports customer payouts
- Eligibility and reward outcomes retain their reasons and version history
- Payout re-checks each account, so changes after opening and prior rewards are caught before the business pays out

---

## What's next

The production implementation defines campaign rules in SQL. I've started exploring a YAML-driven implementation so campaign definitions can be maintained as configuration. That version is not deployed.

---

## What I'd do differently

**Check real accounts before the first payout.** Test data proved the logic did what I wrote. Given more time, I'd have partnered with the business to run a select group of real accounts through the new system and confirm the outcomes matched what they expected.

**Give transactions their own mart.** Tracking works from transaction data directly. I'd break that out into a separate table, filtered to the transactions Cash Bonus cares about with the needed columns already attached, and make tracking depend on it, so tracking starts from the right transactions instead of filtering and joining them itself.

**Ship the summary table with the MVP.** Analysts needed one place to see an account's current state across every stage, so questions about a customer could be answered without tracing each stage separately. I'd make it part of the first release.

---

I care as much about being able to explain a decision later as I do about getting the calculation right in the first place.
