# Lab 2 – Creating an Agent

**Module 2 · Creating an agent from a prompt · ~15 min · 1 exercise**

## Objective

Create your first agent in Copilot Studio using a natural-language prompt, configure it inside a solution, and confirm your core authoring surfaces are ready for the exercises ahead.

## Prerequisites

- Lab 0 complete (Copilot Studio trial + developer environment): <https://copilotstudio.microsoft.com>
- Lab 1 complete (agent designed on paper): [Lab 1 – Designing an Agent for a Use Case](lab-01-agent-design.md)

---

### Exercise 2.1 – Create an agent from a prompt (15 min)

*Goal: create your first draft agent directly from a natural-language prompt inside a solution.*

1. Open Copilot Studio: <https://copilotstudio.microsoft.com>.
2. Create a solution before creating the agent:
   - Open **Solutions** by clicking on the three dots under **Tools** and selecting **Solutions**.
   - Select **+ New solution**.
   - Enter **Display name** (for example, `EPPC Agents` or `EPPC 2026`), then create and confirm **Publisher**.
   - Select **Create**.
3. Navigate back to <https://copilotstudio.microsoft.com> and click the **settings wheel** to select your new solution.

![alt text](../Assets/E1_1.png)

4. Select **Create** and describe your agent using one of the prompts below, or use your own use case:

```text
Assist bankers in identifying, investigating, and managing potential fraud and anti-money laundering cases. Help users gather information, understand internal procedures, coordinate investigative activities, and ensure cases are handled consistently and in accordance with bank policies.
```

5. Click the **right arrow** to create the agent.
6. Confirm your core authoring surfaces are available for editing: **Instructions**, **Knowledge**, **Tools**, and **Model**.

**New UI equivalent (optional):** In Copilot Studio (<https://copilotstudio.microsoft.com>) → **New experience**, do the same setup on the **Build** tab. Note the agent is created without a prompt — you configure it directly on the Build tab.

![alt text](../Assets/E1_2.png)

✅ **Checkpoint:** you have a solution and an agent with all authoring surfaces accessible.

---

## Key concepts

Solution-first authoring · prompt-first agent creation · authoring surfaces (Instructions, Knowledge, Tools, Model) · Classic UI vs New UI Build tab.

## Success criteria

- [ ] Agent is created inside a solution (not the default environment).
- [ ] All four authoring surfaces — **Instructions**, **Knowledge**, **Tools**, **Model** — are visible and accessible.
- [ ] I can locate the equivalent surfaces on the **New UI Build tab**.

➡ Next: **[Lab 3 – Instruction Tuning & Grounding](lab-02-instruction-tuning-grounding.md)** · See also **[Lab 8 – the same setup in the new UI](lab-07-old-vs-new-ui.md)**
