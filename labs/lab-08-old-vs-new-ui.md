# Lab 8 – Old UI → New UI: Quick Concept Map

**Reference · ~20 min · 1 comparison exercise**

## Objective

See where your Classic UI skills map to the **new Copilot Studio agent experience** so you can decide which to use.

## Prerequisites

- At least one lab complete in Classic experience (so you have a reference point).
- A tenant where the new experience is available. **Note:** there is **no migration path** — you'll build a *new* agent here, not convert an existing one.

## Background – concept mapping

The new experience consolidates topics, triggers, and branching logic into **Instructions + reasoning** on a single authoring surface. Here's what moved where:

| Classic concept | New equivalent |
|---|---|
| **Topics** | **Instructions** (agent-level) + **Skills** (reusable structured tasks) |
| **Per-topic custom instruction** | **Skill** (write a `.md` file or add directly under Tools & skills) |
| **Topic routing (if/then branches)** | **Reasoning** (the agent decides based on instructions; no explicit nodes) |
| **Agent triggers / agent flows** | **Workflows** (redesigned designer + node-level test) + **agent node** (inline or published) |
| **Child agents** | **Connected agents** (call published agents from a workflow) |
| **Knowledge tabs (per topic)** | **Knowledge** (agent-level, scoped via instructions) |
| **Actions** | **Tools and skills** (connectors, HTTP, custom skills, inline Python) |
| **Settings / Orchestration mode** | **Model** settings (reasoning tier) |
| **Monitor tab** | **Monitor** tab (built into authoring) |

> **Toggle between them:** Classic shows **Topics / Knowledge / Actions / Settings** in left nav. New shows **Build / Preview / Evaluate / Monitor** tabs. Switch with **Try it now** on Classic home page.

> **Control vs. speed:** Classic = deterministic step-by-step (best for compliance). New = faster to build from instructions, but less node-level control. Decide *before* you invest in building.

---

### Exercise 8.1 – Tour the new Build surface and map one task (20 min)

*Goal: see the new layout and confirm concepts move where you expect.*

1. **Enter the new experience:**
   - From Classic home, select **Try it now**.
   - **Create** a new agent (describe its role in a sentence).

2. **Locate the five Build components:**
   - **Instructions:** paste the Role / Objective / Tool-usage / Reasoning pattern from [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md).
   - **Knowledge:** upload the same knowledge source you used in a Classic lab (lab 02).
   - **Tools and skills:** add a connector (e.g., Dataverse) or a simple HTTP action.
   - **Model:** observe the reasoning tier setting (equivalent to Classic Orchestration mode).
   - **Connected agents:** leave empty for now (this is how you call other agents).

3. **Test and compare:**
   - Click **Preview** and ask a question that requires your knowledge + the tool.
   - Compare the answer quality / citations / reasoning to a Classic agent doing the same job.
   - Note: answers cite sources without you wiring per-topic citation rules (the new runtime infers it from instructions).

✅ **Checkpoint:** you mapped Classic concepts to the new surface and saw an end-to-end query. You can now assess: "For my next build, which experience fits my control/speed need?"

**Bonus:** If you want to compare HITL (Human-in-the-Loop) workflows, see the **bonus comparison** below.

---

## Quick reference: HITL workflows in the new UI (bonus comparison)

If you want to quickly see how Classic Human-in-the-Loop (HITL) workflows map to the new experience:

- **Classic:** agent trigger → topic routing → branching nodes → Dataverse action
- **New:** Workflow (redesigned designer) → RFI node (human gate) → Agent node (inline or published) → output

The agent node runs as the **triggering user**, so OBO auth and permission inheritance work automatically (no shared credentials).

---

## Key concepts

Concept mapping (Classic → New) · Instructions + reasoning · Skills (reusable structured tasks) · Build surface (5 components) · Workflows designer · agent node · Connected agents · no migration path · control vs. speed trade-off.

## Success criteria

- [ ] You navigated the new Build surface and mapped 5 Classic concepts to their new homes.
- [ ] You built a preview-worthy agent in the new experience with knowledge and a tool.
- [ ] You can answer: "For my next project—Classic or New, and why?"

## Stretch goals

- If you want to learn more about using workflows in the new UI, complete **[Lab 7 – Monitoring, Testing & Iteration](lab-06-monitoring-testing-iteration.md)**.

## When to choose which experience

| Your need | Choose |
|---|---|
| Fast build from instructions, reasoning-driven, M365 data focus | **New** |
| Deterministic step-by-step control, compliance audit trail, heavily branched flows | **Classic** |
| HITL workflows with human gates + agent handoff | **New Workflows** (better node testing) |
| Complex topic-driven routing with per-topic custom logic | **Classic** |

**Key reminder:** No migration path between Classic and New. Decide *before* building.

➡ Related: **[Lab 1 – Agent Design](lab-01-agent-design.md)** · **[Lab 6 – Approval Gates](lab-07-workflow-approval-gates.md)** · **[Agenda](../docs/agenda.md)**
