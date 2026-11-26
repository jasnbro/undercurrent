# hot parts

*from one person's PC to the production floor*

---

## The problem

At Mercedes-Benz U.S. International, line management and hot-parts staff used a Microsoft Access database to track parts requests and deliveries for the production line.

The database lived on one employee's PC. When that employee left, they emailed it to a colleague with instructions, but the colleague didn't know how to maintain it. A process the production line relied on was dependent on one person's knowledge.

---

## My role

I designed the data model for a replacement web application and worked with production staff to validate its requirements. A development team supporting the company's South Africa plant built the application.

---

## The approach

There was no documentation or original author available. I reverse-engineered the existing Access tables to understand the requirements, then designed a data model compatible with the planned .NET application.

I walked through the model with line management and hot-parts staff, confirming that it captured their actual processes and the information they needed.

---

## Decisions

**Preserve the familiar structure while enforcing relationships.** I retained the shape of the existing tables so staff could recognize the data and validate the design against their workflow. I introduced explicit primary and foreign keys so the database, rather than the person maintaining it, could enforce those relationships.

---

## The risk

Because staff relied on the system to coordinate production, we ran the Access database and the new application in parallel. I helped validate the development team's implementation against the data model and the staff's day-to-day workflow before the switch.

---

## After

- Near real-time visibility of hot parts on the production floor, with automatic updates
- A system no longer dependent on a single PC or employee
- Less manual maintenance of data relationships
- Self-service access for the staff coordinating parts requests and deliveries

---

## What I'd do differently

- **Consider related parts workflows.** Mirroring the existing model helped make the transition manageable, but it also preserved its narrow scope. I'd explore where a more flexible design could support other parts processes.
- **Document how to use and maintain the system.** I'd provide onboarding documentation for managers and staff so knowledge of the new application could be shared and maintained over time.

---

What stays with me about this project is how much knowledge was tied to one person. Replacing Access addressed part of the problem. Making that knowledge accessible to the next person matters just as much.
