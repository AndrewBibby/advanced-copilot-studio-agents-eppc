# Lab 1 — Designing an Agent for a Use Case

**Module 1 · Designing reliable agents · ~20 min · pen-and-paper / whiteboard**

> Work solo or in pairs. No Copilot Studio clicking — you're producing a design you could hand to a builder.

---

## Ideas before building

The most expensive mistakes in agent development happen in the first ten minutes — before anyone opens the product. Here are the three ideas that matter most:

**1. Architecture beats prompting.**  
When instructions grow long, that's a signal to *split the agent*, not to add more text. A well-scoped specialist with 150 words of instructions outperforms a generalist with 1,500. Design the responsibilities first.

**2. Specialists over generalists.**  
Each agent should have *one job*. One knowledge source, or group of related knowledge sources. One clear boundary. When a single agent owns IT answers, HR answers, ticket-logging and user escalation, it will route badly and hallucinate confidently. Split the jobs, then connect the pieces.

**3. The three link types define your governance.**  
- **Child / sub-agent** — same team, same lifecycle, inherits parent's security and settings. Simplest to build; hardest to reuse.  
- **Connected agent** — independent team, own knowledge and security, invoked as a tool. ⚠ Shared means *shared changes* — updating it affects everyone using it.  
- **A2A** — external org or vendor, open protocol, independent identity. Use when you cross an organisational boundary.

Getting the link type wrong costs you a rearchitecture, not a prompt edit.

---

## Your deliverable

One page (or one whiteboard section) covering:

1. The jobs the agent must do
2. Build surface choice (and why)
3. Single agent or a team — and the link types
4. One knowledge source per specialist
5. A one-sentence role for each agent

---

## The use case

**Employee Service Desk Agent.**  
An employee messages in Teams: *"My VPN won't connect — and what's our remote-work policy?"*  
One message, two domains (IT + HR), and the business also wants a support ticket logged automatically. The answer must arrive as a **single reply**.

> **Swap it if you prefer:** Power Platform governance (find and clean up orphaned flows), contract processing (extract → validate → route), or a real scenario from your own work.

---

## Design Sprint (17 minutes)

### Sprint 1 — Frame the jobs (5 min)

Write down:

1. The use case in **one sentence**: who asks, on what channel, what outcome they expect.
2. The **distinct jobs** in the request. For the service desk: answer an IT question / answer an HR question / log a ticket.
3. For each job: what **data** does it need, and does it **read** or **write**?

> Write actions (create, update, delete) are candidates for a human checkpoint. Flag them now.

**Checkpoint:** a short list of jobs, each with its data source and read/write flag.

---

### Sprint 2 — Pick the build surface and architecture (7 min)

**Build surface — walk this decision tree top-down, take the first yes:**

| Question | Yes → build here |
|----------|-----------------|
| Need pro-code, custom models, evaluation, or large scale? | **Microsoft Foundry** |
| Need explicit, deterministic, scripted conversation control? | **Copilot Studio · Classic UI** |
| Need enterprise tools, connectors, MCP, or multi-agent? | **Copilot Studio · New UI** |
| None of the above | **Agent Builder** |

**Single agent or a team?**  
Split when routing becomes unreliable — too many roles, too many tools. The gains: sharper routing accuracy, smaller scopes that evolve independently, and the ability to add specialists without redesigning the whole thing.

**Sketch the boxes:**

- Name the **orchestrator** (the only agent that talks to the user).
- Name each **specialist** — one job each.
- Label each link: child / connected / A2A.
- Assign **one non-overlapping knowledge source** per specialist.

**Checkpoint:** a labelled sketch with named agents, link types, and one source each.

---

### Sprint 3 — Write the briefs (5 min)

Use the **four-block pattern** (Role / Objective & task flow / Routing rules / Grounding):

**Orchestrator brief (write this one in full):**

> *"You are [name], the [role], and the ONLY agent that responds to the user. When a message arrives: invoke [Specialist A] for [intent], invoke [Specialist B] for [intent], log a ticket via [tool] — then combine all results into EXACTLY ONE reply. Never reply until all specialists have returned findings. Never use recall; always retrieve. If a specialist returns an error, surface it clearly."*

**Specialist brief (one sentence per specialist):**

> *"You are [name], a sub-agent. You MUST NOT reply to the user. Return ONLY findings to the parent orchestrator. Use ONLY [single knowledge source]. If you cannot answer from that source, say so."*

Strong language — **MUST / NEVER / ONLY** — is intentional. Vague directives produce vague agents.

**Checkpoint:** one orchestrator brief + a one-sentence brief per specialist.

---

## Worked example (Employee Service Desk)

| Decision | Answer |
|----------|--------|
| Build surface | Copilot Studio · New UI (needs MCP + multi-agent) |
| Architecture | Orchestrator + 2 sub-agents (HR, IT) + MCP tool |
| Pattern | Single orchestrator — fan-out, merge, single reply |
| HR knowledge | SharePoint policy site |
| IT knowledge | Azure AI Search knowledge base |
| Write tool | Dataverse `create_record` — flag for human checkpoint |

**Orchestrator role:** *"You are the service-desk orchestrator and the ONLY agent that replies to the employee. Route IT questions to the IT agent, HR-policy questions to the HR agent, log a ticket via the MCP tool, then combine everything into ONE reply that includes the ticket number."*

---

## Design review checklist

Run this before moving on:

- [ ] Build surface chosen via the decision tree (first "yes" wins)
- [ ] Each agent has **one clear job**
- [ ] Link types are correct (child / connected / A2A)
- [ ] **One non-overlapping** knowledge source per specialist
- [ ] Orchestrator brief says *"only I respond to the user"*
- [ ] Every specialist brief says *"return findings, don't reply"*
- [ ] Write/irreversible actions flagged for a human checkpoint
- [ ] No catch-all routing rule that swallows a specialist's job

---

## Stretch goals

- Redesign for a different build surface — what do you trade?
- Add an A2A teammate (external supplier, booking agent) and note the governance implications.
- What happens when someone sends an off-domain question? Where would your design break, and what prevents it?

---

## Key concepts

Build surface decision tree · specialists over generalists · child vs connected vs A2A · orchestration patterns (single orchestrator, sequential pipeline, hierarchical, collaborative) · four-block instruction pattern · Single Response Principle · governance & ownership

---

➡ **Next: [Lab 2 — Creating an Agent](lab-02-creating-an-agent.md)**  
Apply your instructions hands-on in the **[new UI in Lab 8](lab-07-old-vs-new-ui.md)**
