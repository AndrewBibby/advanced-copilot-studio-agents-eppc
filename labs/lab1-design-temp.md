# Lab 1 — Designing an Agent for a Use Case (Theory & Design)

**Module 1 · Designing reliable agents · ~60 min · 4 design exercises (≤15 min each)**

> **Format:** this is a **pen-and-paper / whiteboard** design lab — no Copilot Studio clicking. You'll produce an agent *design* you could hand to a builder. Work solo or in pairs; you'll compare designs at the end.

## Objective

Take a real-world use case and produce a complete agent design: **where to build it**, whether it's **one agent or a team**, the **architecture and orchestration pattern**, the **knowledge and tools** each agent needs, and **design-level instructions** with clean handoffs.

## Why design first

Design decisions are far cheaper to get right on paper than to refactor in the product. *"When prompts get long, that's a signal to split the agent — not to add more instructions."* Architecture beats prompting: scope responsibilities, choose the right build surface, and decide single-vs-multi **before** you build.

## Your deliverable — a one-page agent design

By the end you'll have:

1. A **build-surface decision** (and why).
2. A **single-vs-multi-agent** call.
3. An **architecture sketch** (orchestrator + specialists, or one agent) labelled with the right terms.
4. An **orchestration pattern** choice.
5. A **knowledge & tool map** — one source per specialist, plus any write actions that need a human checkpoint.
6. **Instruction briefs** — a four-block parent brief and short sub-agent briefs.
7. A **governance & ownership** note.

---

## The use case

**Primary — Employee Service Desk Agent.** An employee messages the agent in Teams: *"My VPN won't connect, and what's our remote-work policy?"* One message, two domains (an **IT** issue and an **HR** policy question), and the business also wants a **support ticket logged** automatically. Answers must be grounded, governed (RBAC-scoped, audited), and arrive as a **single** reply.

> **Pick a different use case if you prefer** (same exercises apply):
> - **Power Platform governance** — discover, inventory and safely delete *orphaned* flows/agents/apps (owner is a disabled user).
> - **Contract processing** — extract fields → validate → summarise → route for approval.
> - **Cross-org procurement** — your approval workflow calls a supplier's external agent to check stock and pricing.
> - **Bring your own** — a real scenario from your work.

---

### Exercise 1.1 — Frame the use case & list the jobs (15 min)

*Goal: turn a fuzzy request into discrete, designable jobs.*

1. Write the use case in **one sentence**: who asks, on what **channel**, what outcome they expect.
2. List the **distinct jobs / intents** in the request (for the service desk: *answer an IT question*, *answer an HR-policy question*, *log a ticket*).
3. For each job, note the **data it needs** (e.g. IT knowledge base, HR policy site, a ticketing system) and whether it **reads or writes**.

✅ **Checkpoint:** a short list of jobs, each with its data source and read/write flag.

### Exercise 1.2 — Decide where to build & single-vs-multi (15 min)

*Goal: choose the build surface and whether this is one agent or a team.*

1. **Where to build** — walk the decision tree top-down and take the first **yes**:
   - **Q1** Need pro-code, custom models, evaluation or large scale? → **Microsoft Foundry**
   - **Q2** Need explicit, deterministic, scripted conversation control? → **Copilot Studio · Classic UI**
   - **Q3** Need enterprise tools, connectors, MCP or multi-agent? → **Copilot Studio · New UI**
   - **Otherwise** → **Agent Builder** (quickest path for a simple M365 agent).
2. **One agent or a team?** Apply the split test — split when a single agent has **too many roles/tools** to route reliably. Weigh the four gains: **accuracy** (sharper tool routing), **maintainability** (smaller scopes evolve faster), **scalability** (add specialists without redesign), **performance** (activate only what's needed).
3. Record your decision in 2–3 sentences.

✅ **Checkpoint:** a justified build surface and a single-vs-multi call.

### Exercise 1.3 — Architecture, pattern & knowledge/tool map (15 min)

*Goal: lay out the agents, the pattern that connects them, and what each can see and do.*

1. If multi-agent, name the **orchestrator** and each **specialist** — **one job each**.
2. Choose the **architecture** per specialist (rule of thumb):
   - same team & lifecycle → **child / sub-agent** (shares parent's knowledge, tools, security; inherits settings)
   - different team, same platform → **connected agent** (own knowledge/security/governance; invoked as a tool; ⚠ shared agent = shared changes)
   - external org / vendor → **A2A** (open protocol, independent identity & lifecycle)
3. Choose an **orchestration pattern** and justify it:
   - **Single orchestrator** (planner fans out, merges — most common)
   - **Sequential pipeline** (each output feeds the next)
   - **Hierarchical** (manager → team-leads → workers)
   - **Collaborative / A2A** (peers across vendor boundaries)
4. **Map knowledge & tools** — **one non-overlapping source per specialist** (e.g. HR → SharePoint, IT → Azure AI Search) and any **tool/MCP actions** (e.g. log a ticket in Dataverse/ServiceNow). Flag **write actions** that need a human checkpoint (sets up Lab 4).
5. **Sketch** the boxes and arrows.

✅ **Checkpoint:** a labelled architecture diagram + named pattern + a one-source-per-agent map.

### Exercise 1.4 — Instruction briefs, handoffs & governance (15 min)

*Goal: write the design-level instructions and make ownership explicit.*

1. Write the **parent / orchestrator brief** using the **four-block pattern** (see [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md)):
   - **Role** — orchestrator identity; *"you are the ONLY agent that talks to the user."*
   - **Objective & task flow** — invoke specialists → wait for all → combine → deliver **exactly one** reply.
   - **Tool-usage / routing rules** — which specialist handles which intent (route on description).
   - **Reasoning & grounding** — always retrieve, never recall; surface errors.
2. Write a one-paragraph **sub-agent brief** for each specialist: *"You are a sub-agent. You MUST NOT reply to the user. ONLY return findings to the parent. Use ONLY {single source}."* Use strong language — **MUST / NEVER / ONLY**.
3. Note the **handoff points** and confirm the **Single Response Principle** (one combined reply).
4. **Governance & ownership** — who owns each agent, who can change it, what happens when the owner leaves, and the **shared-agent change risk** (updating a connected agent affects everyone using it).
5. Run the **design review checklist** below.

✅ **Checkpoint:** parent + sub-agent briefs, named handoffs, and an ownership note that passes the checklist.

---

## Design review checklist

- [ ] Build surface chosen via the decision tree (first "yes" wins).
- [ ] Each agent has **one clear job** — specialists over generalists.
- [ ] Architecture term is correct for each link (child / connected / A2A).
- [ ] One **non-overlapping** knowledge source per specialist.
- [ ] Orchestration pattern named and justified.
- [ ] Parent brief states *"only I respond to the user"*; every sub-agent says *"return findings, don't reply."*
- [ ] Strong directive language (MUST / NEVER / ONLY).
- [ ] Write/irreversible actions flagged for a human checkpoint.
- [ ] Every agent has an accountable **owner** and a lifecycle plan.
- [ ] No catch-all routing rule that swallows a specialist's queries.

## Worked fragment (Employee Service Desk)

- **Build surface:** Copilot Studio · New UI (Q3 — needs MCP + multi-agent).
- **Architecture:** Orchestrator + two **sub-agents** (HR, IT) + an **MCP tool** to log a ticket.
- **Pattern:** Single orchestrator (fan-out, merge).
- **Knowledge:** HR → SharePoint policy site; IT → Azure AI Search KB (non-overlapping).
- **Tool:** Dataverse/ServiceNow `create_record` (write → human-checkpoint candidate).
- **Parent brief (Role):** *"You are the service-desk orchestrator and the ONLY agent that replies to the employee. Route IT questions to the IT agent, HR-policy questions to the HR agent, log a ticket via the MCP tool, then combine everything into ONE reply with the ticket number."*

---

## Key concepts

Where to build (four ways + decision tree) · specialists over generalists · child vs connected vs A2A · orchestration patterns · the four-block instruction pattern · Single Response Principle · architecture over prompts · governance & ownership.

## Success criteria

- [ ] A complete **one-page design** for your use case.
- [ ] Build surface and single-vs-multi are **justified**, not assumed.
- [ ] Architecture and pattern use the **correct terms**.
- [ ] Parent + sub-agent **briefs** follow the four-block pattern and the Single Response Principle.
- [ ] Ownership and shared-change risk are addressed.

## Stretch goals

- Re-design the same use case for a **different build surface** and list what you'd trade.
- Add an **A2A teammate** (e.g. an external supplier or booking agent) and show the governance implications.
- Stress-test with an **off-domain** question — where would your design hallucinate or break role, and how does the design prevent it?

## Facilitator note

This replaces the earlier hands-on *prompt-refinement* Lab 1. The instruction-tuning, grounding and custom-prompt **hands-on** now lives in **Module 2 — Instructions, Knowledge & Prompts**; use [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md) and [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md) there.

➡ Next: **[Lab 2 — Extend with Dataverse MCP & tools](lab-02-dataverse-mcp-tools.md)** · Apply your instructions hands-on in the **[new UI in Lab 6](lab-06-old-vs-new-ui.md)**
