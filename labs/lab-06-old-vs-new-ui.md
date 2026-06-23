# Lab 6 — Old UI → New UI: The Same Tasks in the New Agent Experience

**Cross-cutting · ~60 min · 3 exercises (≤20 min each)**

## Objective

Re-create two earlier labs in the **new Copilot Studio agent experience** and see exactly where it differs from the Classic UI:

- **Lab 1** (refine prompts at agent & topic level) → done with **Instructions + a Skill** instead of topics.
- **Lab 4** (human-in-the-loop) → done with the **new Workflows designer + agent node** instead of Classic agent flows/triggers.

You'll leave able to decide *which experience to use for which job*.

## Prerequisites

- Labs 1 and 4 complete in the Classic experience (so you have a "before" to compare against).
- A tenant where the new experience is available. **Note:** there is **no migration path** between Classic and New — you'll build a *new* agent here, not convert your existing one.

## Background — what actually changed

The new experience replaces topics, triggers and node-based conversation logic with a **single agent object driven by instructions and reasoning**, all on one consolidated surface.

| | Classic experience | New experience |
|---|---|---|
| Left nav / tabs | **Topics, Knowledge, Actions, Settings** (separate) | **Build · Preview · Evaluate · Monitor** (one surface) |
| Behaviour driven by | Explicit topics, triggers, branching nodes | **Instructions + reasoning** |
| Reusable behaviour | A Topic | A **Skill** (reusable structured behaviour) |
| Triggers / automation | Agent triggers + agent flows | **Workflows** (redesigned designer, node-level testing) + agent node |
| Sub-agents | Child agents | **Connected agents** |
| Orchestration | Classic *or* generative (configurable) | Enhanced runtime for all agents (not switchable) |
| Evaluate / Monitor | Separate step | Built into the authoring surface |

> **How to tell which you're in:** Classic shows **Topics / Knowledge / Actions / Settings** in the left nav. New shows **Build / Preview / Evaluate / Monitor** tabs at the top. Switch with **Try it now** on the Classic home page; switch back with the **New experience** toggle.

> **The trade-off:** Classic gives deterministic, node-by-node control (best for compliance-critical, branching flows). New is faster to build and reasons from natural-language instructions, but is less explicitly controllable. Choose on your need for **control vs. speed**.

---

### Exercise 6.1 — Create a new-experience agent & set up Build (15 min)

*Goal: get oriented on the single-surface model.*

1. On the Classic home page, select **Try it now** to enter the new experience, then **Create** a new agent. Describe its purpose in natural language when prompted.
2. **Before first save**, set the **language** and default **Solution** (still important in the new UI).
3. On the **Build** tab, find the five components: **Instructions**, **Knowledge**, **Tools and skills**, **Model**, **Connected agents**. Add the *same narrow knowledge source* you used in Lab 1.

✅ **Checkpoint:** you can name where each Classic concept now lives on the Build tab.

### Exercise 6.2 — Redo Lab 1 with Instructions + a Skill (20 min)

*Goal: achieve Lab 1's outcome without topics.*

1. In **Instructions**, apply the same Role / Objective / Tool-usage / Reasoning & grounding pattern from [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md). In the new experience, instructions + reasoning replace topic routing.
2. Where Lab 1 used a **per-topic custom instruction**, create a **Skill** instead — a reusable structured behaviour for that specific path (add it under **Tools and skills**; you can write it directly or import a `.md` skill).
3. Apply the grounding intent ("use only specified knowledge", cite sources) through the instructions and knowledge scope, then **Preview** and ask your 5 Lab 1 questions.

✅ **Checkpoint:** answers cite sources and refuse out-of-scope questions — same outcome as Lab 1, achieved with Instructions + a Skill rather than topics.

**Compare:** Classic = topic with Generative Answers custom instructions. New = agent Instructions + a Skill. Note which felt faster, and which gave you more precise control.

### Exercise 6.3 — Redo Lab 4 with a Workflow + agent node (20 min)

*Goal: achieve Lab 4's HITL outcome in the new designer.*

1. Go to **Flows** → **New workflow** (the redesigned designer with node-level testing). This is the new home for what Classic did with agent triggers/flows.
2. Add a **Request for Information** action for the human checkpoint (same RFI behaviour as Lab 4 — Outlook, structured inputs, first-responder-wins), and branch on the response.
3. Add an **Agent node**: either call a published agent or build an **inline agent for this workflow** (give it instructions, optionally tools/knowledge, and pick the output shape — text or structured). The agent node runs as the **triggering user**, so permissions and least-privilege are honoured automatically.
4. **Preview/test** individual nodes, then run end-to-end.

✅ **Checkpoint:** the workflow pauses for a human, then hands a step to an agent node — the Lab 4 outcome, built on the new Workflows surface.

**Compare:** Classic = agent flow + topic-driven handoff. New = Workflow with RFI + agent node, node-level testing, and structured output tokens for downstream steps.

---

## Key concepts

New agent experience (Build / Preview / Evaluate / Monitor) · Instructions + reasoning replacing topics · Skills (reusable structured behaviour) · Workflows vs. agent flows · agent node (inline vs. published, runs as triggering user) · Connected agents replacing child agents · no migration path · control vs. speed.

## Success criteria

- [ ] You built a **new-experience** agent and located each Classic concept on the Build tab.
- [ ] You reproduced **Lab 1's** outcome with **Instructions + a Skill** (no topics).
- [ ] You reproduced **Lab 4's** HITL outcome with a **Workflow + RFI + agent node**.
- [ ] You can state, for a given scenario, whether you'd choose Classic or New and why.

## Decision guide — which experience for which job

- **Choose New** for fast, reasoning-driven agents over M365 data, multi-step orchestration, and where built-in Evaluate/Monitor helps the loop.
- **Choose Classic** when you need deterministic, auditable step-by-step control (compliance-critical, regulated, heavily branched flows), or a feature only Classic currently exposes.
- **Remember:** no migration path, and Classic agents don't appear as connected agents in New (or vice-versa). Decide the experience *before* you invest in building.

➡ Related: **[Lab 1](lab-01-refine-prompts.md)** · **[Lab 4](lab-04-human-in-the-loop.md)** · **[agenda & UI orientation](../docs/agenda.md)**
