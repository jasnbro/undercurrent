# disputes data refactor

*making disputes data easier to work with*

---

## The problem

At Cash App, disputes reporting relied on a pair of versioned tables with more than 50 columns covering cases, transactions, and customers. The team called them the big nasty. We worked with Snowflake, Prefect, and Google Sheets in 2022–2023.

Three problems made reporting difficult to maintain:

- **Competing identifiers.** Multiple customer and transaction IDs made it unclear which keys to use when joining related data.
- **Legacy data quality.** Joining historical records produced results that were difficult to interpret.
- **Duplicated logic.** Analysts repeatedly wrote the same joins, creating opportunities for reporting logic to diverge.

What concerned me was that two analysts could start with the same data and arrive at different answers simply because they chose different keys.

---

## My role

I led the refactor, working with other engineers and colleagues who brought subject-matter and data analysis expertise.

---

## The approach

We separated cases, transactions, and customers into entity tables with a canonical identifier for each. We cleaned the historical data and built a reporting mart containing the transaction information analysts needed, with the shared joins already handled.

---

## Decisions

**Rebuild the model.** Leaving the tables in place would have required less effort immediately, but analysts would still have been responsible for choosing the right identifiers and maintaining their own versions of the same joins.

**Validate against the source system.** Reconciling the new model against the old tables would have reproduced known gaps. We used source system counts instead.

---

## The risk

The main risk was inaccurate reporting during and after the change. We used source counts to validate the model before cutover and added ongoing data quality checks in Anomalo to monitor it afterward.

---

## After

- Faster reporting queries, with commonly needed transaction information already joined
- Cleaner historical records
- Fewer pipeline incidents related to schema drift
- Shared reporting logic maintained in one place rather than across analyst queries
- Documentation explaining the model and the reasoning behind its design

---

## What I'd do differently

**Plan adoption alongside implementation.** The model was ready before the people using it were. We hadn't communicated the change broadly or in enough detail, which slowed adoption and led to repeated one-on-one conversations.

Next time, I'd communicate the change earlier, publish a migration guide mapping old columns to the new tables, and establish a deprecation date for the old model. I should have given the transition as much thought as the model itself.
