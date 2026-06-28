# Agenda & module overview

**Condensed for experienced builders: 8 focused labs (~20 min each) covering the full agent lifecycle in roughly 2.5 hours (modular — pick what you need).** Each lab is capped at 20 minutes and stands alone; modules are thematic. **No migration path between Classic and New UI** – decide on day one which you'll use.

| # | Module | Labs | Duration | Exercises |
|---|--------|------|----------|-----------|
| 0 | **Setup** | Lab 0 – Environment Setup | ~15 min | 1 |
| 1 | **Design & Build** | Lab 1 – Agent Design (decision exercise)<br/>Lab 2 – Creating an Agent | 17 + 20 = **~37 min** | 1 + 1 |
| 2 | **Extend with Tools & Data** | Lab 3 – Instruction Tuning & Grounding<br/>Lab 4 – Subagent & Dataverse MCP | 20 + 20 = **~40 min** | 2 + 1 |
| 3 | **Govern & Secure** | Lab 5 – Auth, DLP & Entitlement* | **~20 min** | 1 (4 parts) |
| 4 | **HITL Checkpoint** | Lab 6 – Workflow Approval Gates | **~20 min** | 1 |
| 5 | **Monitor & Improve** | Lab 7 – Monitoring, Testing & Iteration | ~20 min | (pending condensing) |
| ✦ | **Optional: UI Choice** | Lab 8 – Old UI → New UI (Concept Map) | **~20 min** | 1 |

---

## Setup – Environment & first agent (15 min)

*Copilot Studio trial, Managed Environments, and a clean workspace.*

**What you'll have ready**
- A trial Copilot Studio environment with Dataverse provisioned.
- Managed Environment enabled (required for MCP).
- One solution ready for hands-on work.

➡ **[Lab 0 – Environment Setup](../labs/lab-00-environment-setup.md)**

---

## Module 1 – Designing & building reliable agents (~37 min)

*Decide your architecture; build and configure your first agent.*

**Core ideas**

- **Single job, narrow scope** – agents work best when they own one task; job framing drives architecture.
- **Single vs. multi-agent trade-off** – when to build specialist subagents vs. expanding one agent's capabilities.
- **Four-block instruction pattern** – Role / Objective & task flow / Tool-usage rules / Reasoning & grounding rules. Tight instructions reduce hallucinations.
- **The Build surface** – Instructions, Knowledge, Tools & skills, Model settings, Connected agents. Everything on one page.
- **Grounding dials** – "use only specified knowledge", set moderation level, cite sources. These are the knobs that prevent out-of-scope answers.

**Lab 1 (~17 min):** Design exercise. You and a partner frame a job, decide single vs. multi-agent, sketch the architecture, decide where tools live.

**Lab 2 (~20 min):** First hands-on build. Create a solution, build an agent from a natural-language prompt, confirm all Build surfaces are wired (Instructions, Knowledge, Tools, Model).

➡ **[Lab 1 – Agent Design](../labs/lab-01-agent-design.md)** · **[Lab 2 – Creating an Agent](../labs/lab-02-creating-an-agent.md)**

---

## Module 2 – Extending with tools & data (~40 min)

*Instructions that guide tool use; MCP and Dataverse for read-only specialist agents.*

**Core ideas**

- **The four-block instruction pattern** – Role / Objective & task flow / Tool-usage rules / Reasoning & grounding rules. Clean tool guardrails prevent misuse.
- **Grounding dials** – "use only specified knowledge", moderation level, cite sources. These switch on precision and prevent hallucinations.
- **Subagent discipline** – narrow role, narrow tools, clear invocation intent from the parent. One specialist per concern.
- **MCP as a runtime capability layer** – a universal adapter that makes Dataverse queryable to agents. Treat MCP "like APIs with admin access, not documents."
- **The Dataverse MCP server** – schema discovery, read-only queries (`search_data`, `read_query`), and guarded writes (`create_record`, `update_record` with explicit scoping). RBAC always applies via OBO authentication.
- **Least-privilege data access** – expose only what the agent needs; delete operations require explicit design decisions; use endpoint filtering in DLP to further narrow scope.

**Lab 3 (~20 min):** Instruction tuning. Rewrite instructions using the four-block pattern; set grounding dials (knowledge-scoped, moderation level, citations). Test before/after with baseline queries.

**Lab 4 (~20 min):** Build a specialist subagent wired to Dataverse MCP. Create the MCP server, scope read-only tools, establish inheritance patterns for permission checks, test end-to-end with the parent agent.

➡ **[Lab 3 – Instruction Tuning & Grounding](../labs/lab-03-instruction-tuning-grounding.md)** · **[Lab 4 – Subagent & Dataverse MCP](../labs/lab-04-subagent-Dataverse-mcp.md)**

---

## Module 3 – Governing & securing agents (~20 min)

*DLP discovery exercise; OBO authentication; connector risk matrix.*

**Core ideas**

- **Authentication: OBO is the key** – On-behalf-of (OBO) authentication means agents call connectors *as the signed-in user*, so RBAC is inherited automatically. No shared credentials = no permission leakage.
- **DLP is block-by-default** – environment-level policies that deny all connectors, then allow only what you need. This prevents "connector sprawl."
- **Connector risk matrix** – 10 key connectors across 4 environment tiers (Dev / Test / Internal Prod / External Prod) with Allow/Block/Conditional guidance. Know your risk posture.
- **Common DLP pitfalls** – Managed Environment must be enabled *before* MCP; DLP is environment-scoped (affects all agents); OBO doesn't work on HTTP/Bing/Skills; policy promotions fail silently; start restrictive, add only what works.
- **Environment strategy** – tier by audience and risk. All Managed Environments. Direct Line agents get external DLP rules.

**Lab 5 (~20 min):** Discovery-based exercise. Audit your environment (see: no DLP, all connectors available) → create a restrictive DLP policy (block all, allow-list Dataverse + essentials) → attempt adding blocked connectors to the agent and watch DLP stop you → configure OBO on Dataverse and test permission inheritance. Includes **connector reference matrix** (10 connectors × 4 tiers) and **7 common pitfalls** for DLP + OBO.

➡ **[Lab 5 – Auth, DLP & Entitlement](../labs/lab-05-auth-dlp-entitlement.md)**

---

## Module 4 – Human-in-the-loop (HITL) approval gates (~20 min)

*Pause automation; insert human checkpoints; approve/reject branching.*

**Core ideas**

- **Automation ≠ autonomy** – writes (create/update/delete) should have a human gate, especially when money, compliance, or contracts are involved.
- **Request for Information (RFI)** – pause a workflow, send an email to a named human with structured input (approve/reject + comments), resume when they respond. First responder wins.
- **Approval branching** – if approved: execute the gated write. If rejected: stop and inform the user. Comments are captured for audit.
- **Async approval** – the workflow pauses; the human reviews on their schedule; the workflow resumes when done. The agent doesn't block.

**Lab 6 (~20 min):** Build and test an approval gate workflow. Create an RFI node, configure it to pause and email a reviewer, add approval branching (approve = create account; reject = stop), capture comments for audit, test end-to-end from the agent triggering the workflow.

➡ **[Lab 6 – Workflow Approval Gates](../labs/lab-07-workflow-approval-gates.md)**

---

## Module 5 – Monitor, test & improve (~20 min)

*Closing the agent lifecycle loop.*

**Core ideas**

- **Copilot Studio Kit** – batch testing, test types (response/attachment/generative match), rubrics for scoring generative answers, Compliance Hub & KPIs.
- **Eval gates in CI/CD** – run Kit test sets in a pipeline; fail the build when scores drop below threshold; pair with `pac` ALM commands.
- **Monitor in two places** – per-agent Copilot Studio analytics and fleet-wide Agent 365 observability.
- **The agentic improvement loop** – Analyze → Adjust → Re-test → Ship & repeat.

**Lab 7 (~20 min):** (Pending condensing to 20 min; currently ~60 min across 3 exercises.)

➡ **[Lab 7 – Monitoring, Testing & Iteration](../labs/lab-06-monitoring-testing-iteration.md)**

---

## ✦ Optional – Old UI → New UI (20 min)

*Concept map from Classic experience to the new UI; decide which to use for your next project.*

**Core ideas**

- **No migration path** – Classic and New are separate. Decide *before* investing in one.
- **Control vs. speed trade-off** – Classic = deterministic step-by-step (best for compliance). New = faster to build from instructions, but less node-level control.
- **Where concepts moved** – Topics → Instructions + Skills; Triggers → Workflows + agent node; Child agents → Connected agents.
- **Both experiences are production-ready** – your choice depends on your control/speed priority and feature availability.

**Lab 8 (~20 min):** Quick concept-mapping exercise. Enter the new experience, locate the 5 Build components (Instructions, Knowledge, Tools & skills, Model, Connected agents), paste instructions from the template, add a knowledge source and a tool, preview an agent query, and assess: "For my next project—Classic or New?"

➡ **[Lab 8 – Old UI → New UI (Concept Map)](../labs/lab-08-old-vs-new-ui.md)**

---

## Your path through the labs

- **Cohort-led (~3 hours):** Labs 0 → 1 → 2 → 3 → 4 → 5 → 6 → 7 (skip Lab 8 unless UI choice is your blocker).
- **Pick & choose (modular):** Each lab stands alone; prerequisites are listed. Skip what you know; deep-dive what's new.
- **Optional:** Lab 8 if you're deciding between Classic and New UI.

**One key decision on day one:** Classic or New UI? Most attendees run both labs in parallel to decide; you only commit after Lab 0.
