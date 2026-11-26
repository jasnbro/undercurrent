# How to work with me

> **Short version:** I'm a data systems engineer. I build pipelines, data models, and tools that make complicated work easier to do and maintain. I do my best work when I understand the problem, have room to exercise technical judgment, and work with people who are willing to share what they know.

---

## <i data-lucide="workflow"></i> What I'm good at

I enjoy both designing systems and building them. Working close to the code helps me understand where a design holds up in practice and where it needs to change.

- data pipelines and ingestion
- data modeling
- workflow orchestration
- data quality and operational reliability
- Python and SQL backend work
- turning repeated processes into reusable tools
- making legacy and under-documented systems easier to maintain

When someone brings me a data problem, I want to understand where the data comes from, how it's used, who depends on it, and what the team will need to maintain over time. Sometimes the most useful change is outside the pipeline itself.

**In practice:** I built PipelineTools after noticing the same database connectors, credential handling, environment setup, and project scaffolding repeated across my team's ETL scripts. I consolidated that code into a shared Python library so changes could be made in one place. The library is in production, supporting a YAML-configured batch process and an API integration. Sharing the code also meant a breaking change could affect multiple pipelines, so I paired the library with a managed Python environment to help contain that risk.

---

## <i data-lucide="wrench"></i> What I believe about systems

Good infrastructure reduces the attention people have to spend on it. I want the people using a system to understand how it works, trust its output, and know what to do when something goes wrong.

That's the idea behind **undercurrent**: systems that sit underneath work and life and carry some of the load.

A few principles guide my work:

- **Tables and pipelines are interfaces for people.** Make the grain, column definitions, and expected behavior clear to the people who rely on them.
- **Documentation is part of the system.** The next engineer should be able to understand what exists, why decisions were made, and what has already been tried.
- **Complexity should serve a purpose.** I use a one-page explanation as a check on whether a pipeline's design is understood well enough.
- **Failures should be easy to investigate.** Logs should help identify what failed, where it happened, and which data was affected without requiring someone to recreate the problem.
- **Standards should have a reason.** A team should understand what a standard addresses, why it matters, and how to apply it. If that isn't clear, it's worth revisiting the standard or how it's taught.

---

## <i data-lucide="message-square-text"></i> Communication and feedback

I'm direct and curious. When an explanation doesn't hold together, I ask questions. I appreciate working with people who explain their reasoning, challenge my assumptions, and bring expertise I don't have.

I work best when we share context, agree on what we're trying to accomplish, and make tradeoffs explicit. I have opinions, but I'm willing to change my mind when the evidence supports a different approach.

I prefer specific feedback. Instead of:

> "Maybe think about communicating differently."

I'd rather hear:

> "In that meeting, you went three levels deeper than the decision required. The group lost the thread."

That tells me what happened and gives me something concrete to work on.

---

## <i data-lucide="target"></i> Bringing me a problem

I don't need perfect requirements. Bring me in early enough to help understand the problem and shape the solution. Here are some questions I tend to ask:

1. **What are we trying to change?**
2. **Who is this for?**
3. **What do we know so far?**
4. **What do we still need to learn?**
5. **What constraints are we working within?**
6. **Who owns the decision when there's a tradeoff?**
7. **How will we know the solution works?**

We don't need all the answers on day one. Finding them is often part of the engineering work.

I prefer written context for things we can work through independently and meetings for decisions, complicated shared problems, or conversations where nuance matters. A few bullets beforehand help me prepare. I'm sharpest in the morning.

---

## <i data-lucide="sparkles"></i> What brings out my best work

- a meaningful problem to solve
- room to investigate and question assumptions
- ownership of technical decisions and their consequences
- colleagues who share what they know and care about the quality of the work
- constructive disagreement and clear decisions

I bring structure to complicated problems, follow through on implementation, and care about whether the result is useful after I hand it off. I ask for help when I need expertise I don't have.

---

## <i data-lucide="handshake"></i> What I'm looking for

I'm interested in senior engineering roles where I can design and build data systems, work through technical decisions with other engineers, and improve the systems teams already depend on.

I enjoy helping others understand complicated systems and coordinating across teams when it helps the work move forward. I want my primary contribution to remain technical and hands-on.

---

## <i data-lucide="coffee"></i> Outside the code

I garden, cook, write, ride bikes, and run a small home server. I enjoy learning how things work and finding ways to make them work better, whether it's a pipeline, a garden bed, or a recipe.

---

## <i data-lucide="circle-help"></i> Not sure how to approach me?

Bring me what you know, what you don't, and what you're trying to figure out. We can work through it together.

---

*Last updated: November 2026*
