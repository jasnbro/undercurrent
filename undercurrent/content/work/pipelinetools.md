# pipelinetools

*shared code for recurring ETL work*

---

## The problem

I noticed the same database connectors, credential handling, environment setup, and project scaffolding across my team's ETL scripts. New scripts often started as copies of older ones, and each copy changed independently.

I consolidated those recurring pieces into a shared library. A subsequent migration from Python 3.7 to 3.14 made the cost of duplication especially clear: **182 legacy scripts required manual updates**.

---

## The design

I built PipelineTools so pipelines running in the team's managed environment could use the same implementation for:

- database connectors and connection handling
- project scaffolding: folders, files, and repository setup
- credential generation and rotation
- environment variable management

I used a single entry point around patterns the team already knew and added credential generation and rotation. I wanted to make recurring work easier to maintain without introducing a larger framework.

![PipelineTools architecture: pipelines import one shared library with four modules, running on a managed Python environment](/images/pipelinetools-architecture.svg)

---

## Decisions

**Maintain the library within the team.** I considered an externally managed repository, but it lacked clear ownership and a distribution path. Keeping the library within the team gave us responsibility for the code our pipelines depended on.

**Distribute through a shared location.** This was a practical way to make the library available across users and servers. A fix could be made in one place, but the tradeoff was that pipelines would also share the impact of a breaking change.

---

## The risk

Centralizing code concentrates the consequences of a mistake. To help manage that risk, I standardized the Python version and pinned package versions across the team's environment. That gave the library a known set of dependencies and reduced variation between machines. It did not eliminate the need for testing.

---

## In production

PipelineTools supports a YAML-configured batch process and an API integration, including credential rotation and endpoint ingestion.

---

## What I'd do next

- **Add automated tests.** The managed environment is the primary safeguard today. I'd prioritize testing shared behavior before adding more features.
- **Introduce versioned packaging.** I'm evaluating uv for packaging and distribution so pipelines can control when they adopt a new library version.
- **Separate database access from project setup.** I'd make scaffolding optional so a pipeline can use the database connectors without adopting the library's project structure.

---

The point of the library is to make the next Python upgrade one shared change rather than another round of manual fixes.
