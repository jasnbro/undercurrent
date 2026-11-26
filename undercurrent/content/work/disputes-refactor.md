# disputes data refactor

*making disputes data easier to trust and use*

---

## The problem

At Cash App, disputes reporting relied on a pair of versioned tables with more than 50 columns covering cases, transactions, and customers. The team called them the big nasty. We worked with Snowflake, Prefect, and Google Sheets in 2022–2023.

Three things worried me:

- **Maintainability.** The pipeline broke often from schema drift and changing data types, and those breaks were hard to resolve.
- **Accuracy.** Legacy data quality was poor, so the numbers were hard to trust.
- **Ease of use.** Customers and transactions each had more than one ID, and which ones a record carried depended on the legacy code that produced it. Analysts had to work out the keys and rebuild the same joins themselves, and each copy could drift from the others.

---

## My role

I led the refactor, working with other engineers and colleagues who brought subject-matter and data analysis expertise.

---

## The approach

We separated cases, transactions, and customers into entity tables and made every identifier consistently available, instead of whichever ones a legacy code path happened to carry. We cleaned the historical data and built a reporting mart that does the joins correctly once, so analysts no longer had to choose keys themselves.

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
- Fewer pipeline incidents from schema drift and changing data types
- Shared reporting logic maintained in one place rather than across analyst queries
- Documentation explaining the model and the reasoning behind its design

---

## What I'd do differently

**Plan adoption alongside implementation.** The model was ready before the people using it were. We hadn't communicated the change broadly or in enough detail, which slowed adoption and led to repeated one-on-one conversations.

Next time, I'd communicate the change earlier, publish a migration guide mapping old columns to the new tables, and establish a deprecation date for the old model.
